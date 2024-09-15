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
                    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
                    helm repo update
                    helm upgrade --install prometheus-community/kube-prometheus-stack -f values.yaml
                    '''
                }
            }
        }

    }

}