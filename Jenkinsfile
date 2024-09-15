pipeline {
    agent none  // Define no agent globally to handle it at stage level

    stages {
        stage('Initialize Helm') {
            agent {
                docker {
                    image 'alpine/k8s:1.28.13'
                }
            }
            steps {
                withKubeConfig(credentialsId: 'microk8s') {
                    sh '''
                    export XDG_CONFIG_HOME=$PWD/.config
                    export XDG_CACHE_HOME=$PWD/.cache
                    mkdir -p $XDG_CONFIG_HOME $XDG_CACHE_HOME
                    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
                    helm repo update
                    helm upgrade --install my-kube-prometheus-stack prometheus-community/kube-prometheus-stack --version 62.7.0
                    '''
                }
            }
        }

    }

}
