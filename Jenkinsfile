pipeline {
    agent any

    environment {
        ENV_URL = "pipeline.global.com"  //declaring at pipeline will allow all stages to access this cvariable
        SSH_CRED = credentials('SSH_CRED')
    }

    stages {
        stage('One') {     
            steps {
                echo "stage one"
                echo "environment url is ${ENV_URL}"
            }
        }

        stage('two') {   //declaring at stage will be localised to the stage
            environment {
                ENV_URL = "stage2.global.com"
            }
            steps {
                echo "stage two"
                echo "environment url is ${ENV_URL}"
            }
        }

        stage('three') {  //multiple lines for shell commands
            steps {
                sh '''

                  echo hello world
                  echo hi world
                  echo bye world
                  env

                '''
            }
        }
    }
}