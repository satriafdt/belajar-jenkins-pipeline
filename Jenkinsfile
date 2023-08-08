pipeline {
    agent none

    environment {
        AUTHOR = "Satria Finandita"
        EMAIL = "satria.fdt@gmail.com"
        WEB = "https://www.finanditech.com"
    }

    stages {
        stage("Prepare") {
            environment {
                APP = credentials("satria_rahasia")
            }
            
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Author ${AUTHOR}")
                echo("Email ${EMAIL}")
                echo("Web ${WEB}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("App User : ${APP_USR}")
                echo("App Password : ${APP_PSW}")
            }
        }
        
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {

                script {
                    for (int i = 0; i < 10; i++) {
                        echo("Script ${i}")
                    }
                }

                echo("Start Build")
                sh("./mvnw clean compile test-compile")
                echo("Finish Build")
            }
        }

        stage("Test") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                
                script {
                    def data = [
                        "firstName": "Satria",
                        "lastName": "Finandita"
                    ]
                    writeJSON(file: "data.json", json: data)
                }

                echo("Start Test")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }

        stage("Deploy") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Hello Deploy 1")
                sleep(5)
                echo("Hello Deploy 2")
                echo("Hello Deploy 3")
            }
        }
    }

    post {
        always {
            echo "I will always say Hello again!"
        }
        success {
            echo "Yay, success"
        }
        failure {
            echo "Oh no, failure"
        }
        cleanup {
            echo "Don't care success or error"
        }
    }
}

