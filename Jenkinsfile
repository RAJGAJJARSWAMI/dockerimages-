pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:https://github.com/RAJGAJJARSWAMI/dockerimages-.git'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("rajgajjar/my-app:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/rajgajjar/my-app', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
