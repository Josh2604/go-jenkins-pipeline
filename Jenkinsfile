pipeline {
  agent {label "server-web"}
    parameters {
        string(name: 'name_container', defaultValue: 'qa-go-api-rest', description: 'go-jenkins-pipeline')
        string(name: 'name_imagen', defaultValue: 'qa-go-api-rest', description: 'go-jenkins-pipeline')
        string(name: 'tag_imagen', defaultValue: 'latest', description: 'go-jenkins')
        string(name: 'puerto_imagen', defaultValue: '8080', description: 'go-jenkins')
    }
    environment {
        name_final = "${name_container}${tag_imagen}"
    }
    stages {
          stage('stop/rm') {
            when {
                expression {
                    DOCKER_EXIST = sh(returnStdout: true, script: 'echo "$(docker ps -q --filter name=${name_final})"').trim()
                    return  DOCKER_EXIST != ''
                }
            }
            steps {
                script{
                    sh '''
                        sudo docker stop ${name_final}
                        sudo docker rm -vf ${name_final}
                    '''
                    }
                }
            }
        stage('build') {
            steps {
                script{
                    sh '''
                    docker build . -t ${name_imagen}:${tag_imagen}
                    '''
                    }
                }
            }
            stage('run') {
            steps {
                script{
                    sh '''
                        docker run  -it ${name_imagen}:${tag_imagen}
                    '''
                    }
                }
            }
            stage('command') {
            steps {
                script{
                    sh '''
                      docker exec ${name_final} echo 1
                    '''
                    }
                }
            }
        }
    }