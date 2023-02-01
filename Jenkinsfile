pipeline {
    agent any
    environment {
        registryURI = "registry.hub.docker.com/"
        registry = "prakuldip/jenkinsfile_kul_app_trialone"
        registryCredential = "dockerhub_cred"
    }
stages {
        stage('docker image build,push to remote and delete locally') {
            steps{
                script {
                    def kul_app_image = docker.build("${env.registryURI}${env.registry}:$GIT_COMMIT")
                    docker.withRegistry("https://${env.registryURI}",registryCredential){
                        kul_app_image.push()
                    sh "docker image rm '${registryURI}${registry}:$GIT_COMMIT'"
                    }
                }
            }
        }
    }
    post { 
        always { 
            echo 'Deleting Workspace'
            deleteDir() /* clean up our workspace */
        }
    }
}
