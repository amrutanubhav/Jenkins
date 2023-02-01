pipeline {
    agent any

    environment {
        ENV_URL = "pipeline.global.com"  //declaring at pipeline will allow all stages to access this cvariable
        SSH_CRED = credentials('SSH_CRED')
    }

    options {

        buildDiscarder(logRotator(numToKeepStr: '1'))
        disableConcurrentBuilds()
        disableResume()
        timeout(time: 1, unit: 'MINUTES')
    }

    tools {
        maven 'mvn-381'             // tools must be predefined in manage jenkins : maven jdk gradel

    }

    parameters {

            string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

            text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

            booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

            choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

            password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
            
        }
    triggers { 

        cron('H */4 * * 1-5')
        // pollSCM('H */4 * * 1-5')
        }

    
    stages {
        stage('One') {    
             when { 
                branch 'develop' 
                }
            steps {
                echo "stage one"
                echo "environment url is ${ENV_URL}"
                sh "mvn --version"
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