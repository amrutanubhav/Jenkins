pipeline {
    agent {    // we can define agents by labels  <<manage jenkins > nodes > configure a new ec2 instance and set it as an agent . This pipeline runs on the agent based on the label here>>
        label 'ANSIBLE' //agent should have java installed 
    }

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
       stage('Parallel-stage') {
        parallel { 
        stage('One') {    
             when { 
                // branch 'develop'
                // changeset "**/*.js"
                environment name: 'CHOICE', value: 'Two'
                }
            steps {
                echo "stage one"
                echo "environment url is ${ENV_URL}"
                sh "mvn --version"
                sh "hostname"
                sh "sleep 300"
            }
        }

        stage('two') {   //declaring at stage will be localised to the stage
            environment {
                ENV_URL = "stage2.global.com"
            }
            steps {
                echo "stage two"
                echo "environment url is ${ENV_URL}"
                sh "sleep 300"
            }
        }

        stage('three') {  //multiple lines for shell commands
            steps {
                sh '''

                  echo hello world
                  echo hi world
                  echo bye world
                  env
                  sleep 300

                '''
            }
        }
    }
}}}