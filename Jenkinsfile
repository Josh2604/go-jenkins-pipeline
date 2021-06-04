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

    stage('run') {
      steps {
        script {
          sh '''
docker run  -i ${name_imagen}:${tag_imagen}
'''
        }

      }
    }

    stage('command') {
      steps {
        script {
          sh '''
echo "Executing command"
'''
        }

      }
    }

  }
  environment {
    name_final = 'go-jenkins'
    name_imagen = 'go-jenkins'
    tag_imagen = 'latest'
  }
  parameters {
    string(name: 'name_container', defaultValue: 'go-jenkins', description: 'go-jenkins-pipeline')
    string(name: 'name_imagen', defaultValue: 'go-jenkins', description: 'go-jenkins-pipeline')
    string(name: 'tag_imagen', defaultValue: 'latest', description: 'go-jenkins')
  }
}