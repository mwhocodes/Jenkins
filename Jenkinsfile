def username = 'Jenkins'
def gv
pipeline {

    agent any
    parameters{
        choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    environment {
        NEW_VERSION = '1.3.0'
    }
    
    stages {

         stage("init") {
                steps {
                    script {
                        gv = load "script.groovy"
                }
            }
         }
         stage("build") {
                when {
                    expression {
                        BRANCH_NAME == 'develop'
                    }
                }
                steps {
                    script {
                        gv.buildApp()
                }
            }
        }

        stage("test") {
            when {
                expression {
                        params.executeTests
                }
            }
            steps {
                    script {
                        gv.testApp()
                }
            }
        }

        stage("deploy") {

           steps {
                    script {
                        gv.deployApp()
                }
            }
        }
    }
     post {
        always {
            echo 'hello world'
        }
        failure {
            echo 'will email'
        }
    }
}