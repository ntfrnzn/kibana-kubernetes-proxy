# A custom kibana build to use behind a kubernetes api proxy

The critical difference is in the kibana.yml configuration file, setting
 server.basePath: "/api/v1/proxy/namespaces/kube-system/services/kibana-logging"

Unfortunately, this change cannot be made at deploy time using a ConfigMap,
because the node app must perform bundle optimization, taking tens to hundreds
of seconds.  The change must be made during the docker container build so that
startup time remains quick.

See
- https://discuss.elastic.co/t/how-to-avoid-dynamic-bundle-optimization/37367/4
- https://github.com/docker-library/kibana/issues/31
- https://github.com/elastic/kibana/issues/6057
