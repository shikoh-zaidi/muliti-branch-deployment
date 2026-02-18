pipeline {
  agent  {
    label "${LABEL_NAME}"
  }

  environment{
    IMAGE_NAME = "netweb"
    IMAGE_TAG = "${BUILD_NUMBER}"
    CONTAINER_NAME = "net1"
    
  }

  stages{
    stage('checkout'){
      steps{
        git url:"https://github.com/shikoh-zaidi/muliti-branch-deployment.git",branch:"main"
      }
    }
    stage('build'){
      steps{
        sh " docker stop $CONTAINER_NAME || true "
        sh " docker rm $CONTAINER_NAME || true "
        sh " docker run -d --name $CONTAINER_NAME -p 9000:80 --restart always $IMAGE_NAME:$IMAGE_TAG "
        
      }
    }
  }

  post{
    success {
      clean Ws()
    }
    failure{
      echo "pipeline failed"
    }
  }
}
