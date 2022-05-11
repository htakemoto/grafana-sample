# -*- mode: Python -*

# Helm Values

helmValues = read_yaml('./charts/values.yaml')
grafanaPort = int(helmValues['grafana']['grafana.ini']['server']['http_port'])
lokiPort = 3100
promtailPort = 3101

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

k8s_resource('promtail',
  port_forwards=[
    port_forward(promtailPort, promtailPort)
  ],
  labels=['Agent']
)