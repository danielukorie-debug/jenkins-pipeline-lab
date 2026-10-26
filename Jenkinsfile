pipeline {
    agent any

    stages {
        stage('Welcome') {
            steps {
                echo 'Hello! My first Jenkins pipeline is working.'
                echo 'I am learning Docker, Kubernetes, and DevOps.'
            }
        }

        stage('Check') {
            steps {
                echo 'Step 2: My automated job ran successfully!'
            }
        }

        stage('Checkout Kubernetes Manifests') {
            steps {
                dir('kubernetes-manifests') {
                    git branch: 'main',
                        url: 'https://github.com/danielukorie-debug/kubernetes-minikube-lab.git'
                }
            }
        }

        stage('Validate Kubernetes Manifests') {
            steps {
                sh '''
                    set -eu

                    KUBECONFORM_VERSION=0.8.0
                    KUBECONFORM_SHA256=9bc2bffbf71f261128533edaf912153948b7ff238f9a531ae6d34466ec287883

                    mkdir -p .tools

                    curl -fsSL \
                      "https://github.com/yannh/kubeconform/releases/download/v${KUBECONFORM_VERSION}/kubeconform-linux-amd64.tar.gz" \
                      -o .tools/kubeconform.tar.gz

                    echo "${KUBECONFORM_SHA256}  .tools/kubeconform.tar.gz" \
                      | sha256sum --check -

                    tar -xzf .tools/kubeconform.tar.gz \
                      -C .tools kubeconform

                    chmod +x .tools/kubeconform

                    .tools/kubeconform \
                      -strict \
                      -summary \
                      -kubernetes-version 1.37.0 \
                      kubernetes-manifests/deployment.yaml \
                      kubernetes-manifests/service.yaml
                '''
            }
        }
    }
}
