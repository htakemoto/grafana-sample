# -*- mode: Python -*

# Helm Values

helmValues = read_yaml('./charts/values.yaml')
grafanaPort = int(helmValues['grafana']['grafana.ini']['server']['http_port'])
promtailPort = 3101
lokiPort = 3100
elasticsearchPort = 9200
postgresqlPort = int(helmValues['postgresql']['service']['ports']['postgresql'])

# Kubernetes

k8s_yaml(helm(
  'charts',
  name='grafana'
))

k8s_resource('grafana',
  port_forwards=[
    port_forward(grafanaPort, grafanaPort)
  ],
  labels=['UI']
)

k8s_resource('promtail',
  port_forwards=[
    port_forward(promtailPort, promtailPort)
  ],
  labels=['Agent']
)

k8s_resource('loki',
  port_forwards=[
    port_forward(lokiPort, lokiPort)
  ],
  links=[
    link('http://localhost:{}/metrics'.format(lokiPort), 'metrics'),
    link('http://localhost:{}/ready'.format(lokiPort), 'ready')
  ],
  labels=['Database']
)

k8s_resource('elasticsearch',
  port_forwards=[
    port_forward(elasticsearchPort, elasticsearchPort)
  ],
  labels=['Database']
)

k8s_resource('postgresql',
  port_forwards=[
    port_forward(postgresqlPort, postgresqlPort)
  ],
  labels=['Database']
)