pipeline {
  agent any
  stages {
    stage('stop/rm') {
      when {
        expression {
          DOCKER_EXIST = sh(returnStdout: true, script: 'echo "$(docker ps -q --filter name=${name_final})"').trim()
          return  DOCKER_EXIST != ''
        }

      }
      steps {
        script {
          sh '''
sudo docker stop ${name_final}
sudo docker rm -vf ${name_final}
'''
        }

      }
    }

    stage('build') {
      steps {
        script {
          sh '''
docker build . -t ${name_imagen}:${tag_imagen}
'''
        }

      }
    }

    stage('test') {
      steps {
        script {
          sh '''
echo "Im testing"
'''
        }

      }
    }

    stage('command') {
      steps {
        script {
          sh '''
echo "Im executing a command"
'''
        }

      }
    }

  }
  environment {
    name_final = 'go-jenkins'
    name_image = 'go-jenkins'
    tag_image = 'go-jenkins'
  }
}