# external-dns

## Chart Details

This chart will do the following:

* Create a deployment of [external-dns] within your Kubernetes Cluster.

Currently this uses the [Zalando] hosted container, if this is a concern follow the steps in the [external-dns] documentation to compile the binary and make a container. Where the chart pulls the image from is fully configurable.

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release stable/external-dns
```

## Configuration

The following table lists the configurable parameters of the external-dns chart and their default values.


| Parameter                          | Description                                                                                                                         | Default                                            |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| `annotationFilter`                 | Filter sources managed by external-dns via annotation using label selector semantics (default: all sources) (optional).             | `""`                                               |
| `aws.accessKey`                    | `AWS_ACCESS_KEY_ID` to set in the environment (optional).                                                                           | `""`                                               |
| `aws.secretKey`                    | `AWS_SECRET_ACCESS_KEY` to set in the environment (optional).                                                                       | `""`                                               |
| `aws.region`                       | `AWS_DEFAULT_REGION` to set in the environment (optional).                                                                          | `us-east-1`                                        |
| `aws.roleArn`                      | If assume role credentials are used then is the role_arn (arn:aws:iam::....). Leave empty if not used.                              | `""`                                               |
| `aws.zoneType`                     | Filter for zones of this type (optional, options: public, private).                                                                 | `""`                                               |
| `azure.secretName`                 | Set the secret created for the SP for azure, should contain an azure.json file                                                      | `""`                                               |
| `cloudflare.apiKey`                | `CF_API_KEY` to set in the environment (optional).                                                                                  | `""`                                               |
| `cloudflare.email`                 | `CF_API_EMAIL` to set in the environment (optional).                                                                                | `""`                                               |
| `domainFilters`                    | Limit possible target zones by domain suffixes (optional).                                                                          | `[]`                                               |
| `extraArgs`                        | Optional object of extra args, as `name`: `value` pairs. Where the name is the command line arg to external-dns.                    | `{}`                                               |
| `extraEnv`                         | Optional array of extra environment variables. Supply a `name` property and either `value` of `valueFrom` for each.                 | `[]`                                               |
| `google.project`                   | When using the Google provider, specify the Google project (required when provider=google).                                         | `""`                                               |
| `google.serviceAccountSecret`      | When using the Google provider, optionally specify the secret which contains credentials.json if necessary.                         | `""`                                               |
| `image.name`                       | Container image name (Including repository name if not `hub.docker.com`).                                                           | `registry.opensource.zalan.do/teapot/external-dns` |
| `image.pullPolicy`                 | Container pull policy.                                                                                                              | `IfNotPresent`                                     |
| `image.tag`                        | Container image tag.                                                                                                                | `v0.5.7`                                           |
| `image.pullSecrets`                | Array of pull secret names                                                                                                          | `[]`                                               |
| `infoblox.gridHost`                | When using the Infoblox provider, specify the Infoblox Grid host.                                                                   | `""`                                               |
| `infoblox.wapiUsername`            | When using the Infoblox provider, specify the Infoblox WAPI username.                                                               | `""`                                               |
| `infoblox.wapiPassword`            | When using the Infoblox provider, specify the Infoblox WAPI password.                                                               | `""`                                               |
| `infoblox.domainFilter`            | When using the Infoblox provider, optionally specify the domain.                                                                    | `""`                                               |
| `infoblox.noSslVerify`             | When using the Infoblox provider, optionally disable SSL verification.                                                              | `false`                                            |
| `infoblox.wapiPort`                | When using the Infoblox provider, optionally specify the Infoblox WAPI port.                                                        | `""`                                               |
| `infoblox.wapiVersion`             | When using the Infoblox provider, optionally specify the Infoblox WAPI version.                                                     | `""`                                               |
| `infoblox.wapiConnectionPoolSize`  | When using the Infoblox provider, optionally specify the Infoblox WAPI request connection pool size.                                | `""`                                               |
| `infoblox.wapiHttpTimeout`         | When using the Infoblox provider, optionally specify the Infoblox WAPI request timeout in seconds.                                  | `""`                                               |
| `logLevel`                         | Verbosity of the logs (options: panic, debug, info, warn, error, fatal)                                                             | `info`                                             |
| `nodeSelector`                     | Node labels for pod assignment                                                                                                      | `{}`                                               |
| `podAnnotations`                   | Additional annotations to apply to the pod.                                                                                         | `{}`                                               |
| `policy`                           | Modify how DNS records are sychronized between sources and providers (options: sync, upsert-only ).                                 | `upsert-only`                                      |
| `provider`                         | The DNS provider where the DNS records will be created (options: aws, google, azure, cloudflare, digitalocean, inmemory, infoblox). | `aws`                                              |
| `publishInternalServices`          | Allow external-dns to publish DNS records for ClusterIP services (optional).                                                        | `false`                                            |
| `rbac.create`                      | If true, create & use RBAC resources                                                                                                | `false`                                            |
| `rbac.serviceAccountName`          | Existing ServiceAccount to use (ignored if rbac.create=true)                                                                        | `default`                                          |
| `registry`                         | Registry method to use (options: txt, noop)                                                                                         | `txt`                                              |
| `resources`                        | CPU/Memory resource requests/limits.                                                                                                | `{}`                                               |
| `priorityClassName`                | priorityClassName                                                                                                                   | `""`                                               |
| `service.annotations`              | Annotations to add to service                                                                                                       | `{}`                                               |
| `service.clusterIP`                | IP address to assign to service                                                                                                     | `""`                                               |
| `service.externalIPs`              | Service external IP addresses                                                                                                       | `[]`                                               |
| `service.loadBalancerIP`           | IP address to assign to load balancer (if supported)                                                                                | `""`                                               |
| `service.loadBalancerSourceRanges` | List of IP CIDRs allowed access to load balancer (if supported)                                                                     | `[]`                                               |
| `service.servicePort`              | Service port to expose                                                                                                              | `7979`                                             |
| `service.type`                     | Type of service to create                                                                                                           | `ClusterIP`                                        |
| `sources`                          | List of resource types to monitor, possible values are fake, service or ingress.                                                    | `[service, ingress]`                               |
| `tolerations`                      | List of node taints to tolerate (requires Kubernetes >= 1.6)                                                                        | `[]`                                               |
| `affinity`                         | List of affinities (requires Kubernetes >=1.6)                                                                                      | `{}`                                               |
| `txtOwnerId`                       | When using the TXT registry, a name that identifies this instance of ExternalDNS (optional)                                         | `"default"`                                        |
| `txtPrefix`                        | When using the TXT registry, a prefix for ownership records that avoids collision with CNAME entries (optional)                     | `""`                                               |
| `zoneIdFilters`                    | Limit possible target zones by zone id (optional)                                                                                   | `[]`                                               |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/external-dns
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## IAM Permissions

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": [
       "route53:ChangeResourceRecordSets"
     ],
     "Resource": [
       "arn:aws:route53:::hostedzone/*"
     ]
   },
   {
     "Effect": "Allow",
     "Action": [
       "route53:ListHostedZones",
       "route53:ListResourceRecordSets"
     ],
     "Resource": [
       "*"
     ]
   }
 ]
}
```

[external-dns]: https://github.com/kubernetes-incubator/external-dns
[Zalando]: https://zalando.github.io/
[getting-started]: https://github.com/kubernetes-incubator/external-dns/blob/master/README.md#getting-started
