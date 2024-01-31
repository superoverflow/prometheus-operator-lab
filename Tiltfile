load('ext://secret', 'secret_yaml_generic')

allow_k8s_contexts(['colima', 'docker-desktop'])

def setup_sample_app():
    k8s_yaml([
        'k8s/sample-app/deployment.yaml',
        'k8s/sample-app/service.yaml',
        'k8s/sample-app/serviceMonitoring.yaml',
    ])

def install_prometheus_operator():
    prometheus_operator_version='v0.71.2'
    prometheus_operator_bundle=(
        'https://github.com/prometheus-operator/prometheus-operator/releases/download/{version}/bundle.yaml'
    ).format(version=prometheus_operator_version)
    local_resource(
        'download-prometheus-operator-bundle', 
        cmd='wget -c {url}'.format(url=prometheus_operator_bundle))
    k8s_yaml('bundle.yaml')


def setup_alertmanager():
    k8s_yaml('k8s/alertmanager/alertmanager.yaml')
    secret_yaml_generic('alertmanager-example', from_file='k8s/alertmanager/alertRoute.yaml')
    k8s_yaml('k8s/alertmanager/service.yaml')
    k8s_yaml([
        'k8s/alertmanager/prometheus.yaml',
        'k8s/alertmanager/prometheusRule.yaml'
    ])

def setup_prometheus_role():
    k8s_yaml([
        'k8s/prometheus/serviceAccount.yaml',
        'k8s/prometheus/clusterRole.yaml',
        'k8s/prometheus/clusterRoleBinding.yaml',
    ])

def provision_team1():
    k8s_yaml([
        'config/team1/prometheus.yaml',
        'config/team1/prometheusRule.yaml',
        'config/team1/service.yaml',
    ])

def provision_team2():
    k8s_yaml([
        'config/team2/prometheusRule.yaml',
    ])


def main():
    install_prometheus_operator()
    setup_prometheus_role()
    setup_sample_app()
    setup_alertmanager()
    provision_team1()
    provision_team2()
    
main()