/*pipeline {
    agent any
    tools {
        maven 'Maven 3.9.8'
    }
    environment {
        MAVEN_HOME = tool name: 'Maven 3.9.8', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test'){
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}*/


pipeline {
    agent any
    tools {
        maven 'Maven 3.9.8'
    }
    environment {
        MAVEN_HOME = tool name: 'Maven 3.9.8', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Build') {
            agent {
                label 'cimg/openjdk:21.0.2-browsers' // Use the Docker tool configured in Jenkins
            }
            steps {
                script {
                    // Run Docker commands or use Docker images here
                    docker.image('cimg/openjdk:21.0.2-browsers').inside {
                        // Commands to run inside the Docker container
                        sh 'mvn -B -DskipTests clean package'
                    }
                }
            }
        }
        // Additional stages
    }
}
