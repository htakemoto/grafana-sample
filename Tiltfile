# -*- mode: Python -*

# Helm Values

helmValues = read_yaml('./charts/values.yaml')
grafanaPort = int(helmValues['grafana']['grafana.ini']['server']['http_port'])

# Kubernetes

k8s_yaml(helm(
  'charts',
  name='grafana'
))

k8s_resource('grafana',
  port_forwards=[
    port_forward(grafanaPort, grafanaPort)
  ],
  labels=['App']
)