pipeline{
  agent any
  environment{
    DOCKER_HUB_USERNAME = "mukeshjava92"
    APP_NAME = "git-argo-app"
    IMAGE_TAG = "${BUILD_ID}" 
    IMAGE_NAME = "${DOCKER_HUB_USERNAME}"+"/"+"${APP_NAME}"
    REGISTRY_CREDS = 'docker_cred'   
  }
  stages{

        stage( 'Clear the Work Space'){
          steps{
            script{
              cleanWs()
            }
          }
        }
        stage('Checkout SCM'){
          steps{
            git branch: 'main', url: 'https://github.com/mukeshjava92/git_argocd_minikube.git'
            }
          }
        stage('Docker image build'){
          steps{
            script{
            docker_image = docker.build "${IMAGE_NAME}"
            }
            }
          }
          stage('Push image to Dockerhub'){
          steps{
            script{
            docker.withRegistery('',REGISTRY_CREDS){
              docker_image.push("$BUILD_NUMBER")
              docker_image.push('latest')
            }
            }
            }
          }
        }
   }