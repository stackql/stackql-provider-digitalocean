## `digitalocean` provider for [`stackql`](https://github.com/stackql/stackql)

This repository is used to generate and document the `digitalocean` provider for StackQL, allowing you to query and manipulate DigitalOcean resources using SQL-like syntax. The provider is built using the `@stackql/provider-utils` package, which provides tools for converting OpenAPI specifications into StackQL-compatible provider schemas.

The `@stackql/provider-utils` package offers several utilities that this provider uses:
- `split` - Divides a large OpenAPI spec into smaller service-specific files
- `analyze` - Examines OpenAPI specs and generates mapping configuration files
- `generate` - Creates StackQL provider extensions from OpenAPI specs and mappings
- `docgen` - Builds documentation for the provider

### Prerequisites

To use the DigitalOcean provider with StackQL, you'll need:

1. A DigitalOcean account with appropriate API credentials
2. A DigitalOcean personal access token with sufficient permissions for the resources you want to access
3. StackQL CLI installed on your system (see [StackQL](https://github.com/stackql/stackql))

### 1. Download the Open API Specification

First, download the DigitalOcean API OpenAPI specification:

```bash
curl -L https://api-engineering.nyc3.digitaloceanspaces.com/spec-ci/DigitalOcean-public.v2.yaml \
  -o provider-dev/downloaded/digitalocean-public.v2.yaml
```

This downloads the official DigitalOcean API specification, which defines all available API endpoints, request parameters, and response schemas.

### 2. Split into Service Specs

Next, split the monolithic OpenAPI specification into service-specific files:

```bash
npm run split -- \
  --provider-name digitalocean \
  --api-doc provider-dev/downloaded/digitalocean-public.v2.yaml \
  --svc-discriminator tag \
  --output-dir provider-dev/source \
  --overwrite \
  --svc-name-overrides "$(cat <<EOF
{
  "1_click_applications": "oneclick",
  "actions": "account",
  "gradientai_platform": "genai",
  "byoip_prefixes": "network",
  "partner_network_connect": "network",
  "project_resources": "projects",
  "vpc_peerings": "vpcs",
  "spaces_keys": "spaces",
  "uptime": "monitoring",
  "droplets": "compute",
  "droplet_actions": "compute",
  "droplet_autoscale_pools": "compute",
  "cdn_endpoints": "compute",
  "certificates": "compute",
  "domains": "compute",
  "domain_records": "compute",
  "firewalls": "compute",
  "images": "compute",
  "image_actions": "compute",                  
  "load_balancers": "compute",
  "regions": "compute",
  "reserved_ips": "compute",
  "reserved_ip_actions": "compute",
  "[public_preview]_reserved_ipv6": "compute",
  "[public_preview]_reserved_ipv6_actions": "compute",
  "sizes": "compute",
  "ssh_keys": "compute",  
  "tags": "compute",  
  "block_storage": "compute", 
  "block_storage_actions": "compute", 
  "[public_preview]_vpc_nat_gateways": "compute",   
  "snapshots": "compute",
  "functions": "serverless",
  "floating_ips": "network",
  "floating_ip_actions": "network",      
  "container_registries": "container_registries",
  "container_registry": "container_registries"
}
EOF
)"
```

This step breaks down the large DigitalOcean API specification into smaller, more manageable service files. The `--svc-discriminator tag` option tells the tool to use the OpenAPI tags to determine which API endpoints belong to which service. For DigitalOcean, this creates separate files for different functional areas like droplets, volumes, load balancers, etc.

### 3. Generate Mappings

Generate the mapping configuration that connects OpenAPI operations to StackQL resources:

```bash
npm run generate-mappings -- \
  --provider-name digitalocean \
  --input-dir provider-dev/source \
  --output-dir provider-dev/config
```

This step analyzes the service specs and creates a CSV mapping file that defines how OpenAPI operations translate to StackQL resources, methods, and SQL verbs. The mapping process handles two scenarios:

1. **New Provider Development**: If no mapping file exists yet, this creates a new `all_services.csv` file with all operations from the OpenAPI spec. You'll need to edit this file to assign appropriate resource names, method names, and SQL verbs.

2. **Updating Existing Mappings**: If a mapping file already exists, the tool will:
   - Load the existing mappings
   - Identify new operations that aren't yet mapped
   - Flag operations with incomplete mappings (missing resource, method, or SQL verb)
   - Skip operations that are already fully mapped

Update the resultant `provider-dev/config/all_services.csv` to add the `stackql_resource_name`, `stackql_method_name`, `stackql_verb` values for each operation.

### 4. Generate Provider

This step transforms the split OpenAPI service specs into a fully-functional StackQL provider by applying the resource and method mappings defined in your CSV file.

```bash
npm run generate-provider -- \
  --provider-name digitalocean \
  --input-dir provider-dev/source \
  --output-dir provider-dev/openapi/src/digitalocean \
  --config-path provider-dev/config/all_services.csv \
  --servers '[{"url": "https://api.digitalocean.com"}]' \
  --provider-config '{"auth": {"credentialsenvvar": "DIGITALOCEAN_TOKEN","type": "bearer"}}' \
  --overwrite
```

Make necessary updates to the output docs:

```bash
sh provider-dev/scripts/post_processing.sh
```

The `--servers` parameter defines the base URL for API requests. For DigitalOcean, this sets the API endpoint to the v2 API.

The `--provider-config` parameter sets up the authentication method. For DigitalOcean, this configures a bearer token authentication scheme that:
- Looks for the API token in the `DIGITALOCEAN_TOKEN` environment variable
- Uses the token as a bearer token in the Authorization header

The generated provider will be structured according to the StackQL conventions, with properly organized resources and methods that map to the underlying API operations.

After running this command, you'll have a complete provider structure in the `provider-dev/openapi/src` directory, ready for testing or packaging.

### 5. Test Provider

#### Starting the StackQL Server

Before running tests, start a StackQL server with your provider:

```bash
PROVIDER_REGISTRY_ROOT_DIR="$(pwd)/provider-dev/openapi"
npm run start-server -- --provider digitalocean --registry $PROVIDER_REGISTRY_ROOT_DIR
```

#### Test Meta Routes

Test all metadata routes (services, resources, methods) in the provider:

```bash
npm run test-meta-routes -- digitalocean --verbose
```

When you're done testing, stop the StackQL server:

```bash
npm run stop-server
```

Use this command to view the server status:

```bash
npm run server-status
```

#### Run test queries

Run some test queries against the provider using the `stackql shell`:

```bash
PROVIDER_REGISTRY_ROOT_DIR="$(pwd)/provider-dev/openapi"
REG_STR='{"url": "file://'${PROVIDER_REGISTRY_ROOT_DIR}'", "localDocRoot": "'${PROVIDER_REGISTRY_ROOT_DIR}'", "verifyConfig": {"nopVerify": true}}'
./stackql shell --registry="${REG_STR}"
```

Example queries to try:

```sql
-- List all droplets
SELECT 
  id, 
  name, 
  region.slug as region, 
  size.slug as size, 
  status 
FROM 
  digitalocean.droplet.droplets;

-- List all volumes
SELECT 
  id, 
  name, 
  size_gigabytes, 
  region.slug as region 
FROM 
  digitalocean.volume.volumes;

-- List all Kubernetes clusters
SELECT 
  id, 
  name, 
  region_slug, 
  version, 
  status.state 
FROM 
  digitalocean.kubernetes.clusters;
```

### 6. Publish the provider

To publish the provider push the `digitalocean` dir to `providers/src` in a feature branch of the [`stackql-provider-registry`](https://github.com/stackql/stackql-provider-registry). Follow the [registry release flow](https://github.com/stackql/stackql-provider-registry/blob/dev/docs/build-and-deployment.md).  

Launch the StackQL shell:

```bash
export DEV_REG="{ \"url\": \"https://registry-dev.stackql.app/providers\" }"
./stackql --registry="${DEV_REG}" shell
```

pull the latest dev `digitalocean` provider:

```sql
registry pull digitalocean;
```

Run some test queries to verify the provider works as expected.

### 7. Generate web docs

```bash
npm run generate-docs -- \
  --provider-name digitalocean \
  --provider-dir ./provider-dev/openapi/src/digitalocean/v00.00.00000 \
  --output-dir ./website \
  --provider-data-dir ./provider-dev/docgen/provider-data
```  

Make sure to create the provider data directory with appropriate header files:

```bash
mkdir -p ./provider-dev/docgen/provider-data
```

Create `headerContent1.txt`:
```
---
title: digitalocean
hide_title: false
hide_table_of_contents: false
keywords:
  - digitalocean
  - stackql
  - infrastructure-as-code
  - configuration-as-data
description: Query and manage DigitalOcean resources using SQL
---

# DigitalOcean Provider

The DigitalOcean provider for StackQL allows you to query, deploy, and manage DigitalOcean resources using SQL. This provider supports droplets, volumes, Kubernetes clusters, load balancers, and more.
```

Create `headerContent2.txt`:
```
## Authentication

DigitalOcean requires a personal access token for authentication. You can create one in the DigitalOcean control panel under API > Tokens/Keys.

Set your token as an environment variable:

```bash
export DIGITALOCEAN_TOKEN="your_token_here"
```

For more information, see the [DigitalOcean API documentation](https://docs.digitalocean.com/reference/api/).
```

### 8. Test web docs locally

```bash
cd website
# test build
yarn build

# run local dev server
yarn start
```

### 9. Publish web docs to GitHub Pages

Under __Pages__ in the repository, in the __Build and deployment__ section select __GitHub Actions__ as the __Source__. In Netlify DNS create the following records:

| Source Domain | Record Type  | Target |
|---------------|--------------|--------|
| digitalocean-provider.stackql.io | CNAME | stackql.github.io |

## License

MIT

## Contributing

Contributions to the DigitalOcean provider are welcome! Please feel free to submit a Pull Request.