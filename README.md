# cg-s3-proxy

This is an nginx proxy for deployment on Cloud.gov that proxies content from an S3 bucket. It works well with Federalist websites.

The proxy has two configurable routing paths. The first path is to route all requests from a `BASE_DOMAIN` (such as `18f.gsa.gov`) to a specific path on a S3 bucket, defined by `PROXY_ROOT` (such as `http://federalist.18f.gov.s3-website-us-east-1.amazonaws.com/site/18F/18f.gsa.gov`, which in this case is the origin of a Federalist site).

The second is that all other non-`BASE_DOMAIN` requests will route to `PROXY_ROOT/site/$domain`, where `$domain` is the domain of the request. For examples, `https://example.gov/about/` would route to `PROXY_ROOT/site/example.gov/about/`. This enables the proxy to function as a multi-tenent origin proxy for Federalist sites.

## Deployment

Deploy to Cloud.gov by setting the desired environment variables and pushing with `cf push`.

## Configuration

Configuration is handled by environment variables. The following variables are available:

- `BASE_DOMAIN`: Requests on this domain are routed to the root of `PROXY_ROOT`
- `PROXY_ROOT`: The URL from which requests should be proxied; may include subdirectories
- `PORT`: The port on which the server should listen; set automatically by cloud.gov
- `GZIP_COMPRESS`: If `true`, responses will be GZIP'd; False by default since Federalist does this automatically
- `CACHE_EXPIRES`: The value for the `expires` header

### Public domain

This project is in the worldwide [public domain](LICENSE.md). As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
