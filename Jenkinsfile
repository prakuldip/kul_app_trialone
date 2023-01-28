pipeline {
    agent any
    environment {
        registryURI = "https://registry.hub.docker.com/"
        registry = "prakuldip/jenkinsfile_kul_app_trialone"
        registryCredential = "dockerhub_cred"
    }
stages {
        stage('building and pushing docker image') {
            environment {
            registry_endpoint = "${env.registryURI}" + "${env.registry}"
            image_tag = "${env.registryURI}" + ":" + "$GIT_COMMIT"
            }
            steps{
                script {
                    def kul_app_image = docker.build(image_tag)
                    docker.withRegistry(registry_endpoint,registryCredential){
                        kul_app_image.push()
                    }
                }
            }
        }

    }
}