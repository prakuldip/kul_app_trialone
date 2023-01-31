pipeline {
    agent any
    environment {
        registryURI = "registry.hub.docker.com/"
        registry = "prakuldip/jenkinsfile_kul_app_trialone"
        registryCredential = "dockerhub_cred"
    }
stages {
        stage('building and pushing docker image') {
            steps{
                script {
                    def kul_app_image = docker.build("${env.registryURI}${env.registry}:$GIT_COMMIT")
                    docker.withRegistry(registryURI,registryCredential){
                        kul_app_image.push()
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