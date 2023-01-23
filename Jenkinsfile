pipeline {
    agent any

    stages {
        stage('One') {
            steps {
                echo "stage one"
            }
        }

        stage('two') {
            steps {
                echo "stage two"
            }
        }

        stage('three') {
            steps {
                sh '''

                  echo hello world
                  echo hi world
                  echo bye world

                '''
            }
        }
    }
}