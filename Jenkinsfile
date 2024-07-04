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
        maven 'Maven 3.9.8' // Define Maven tool installation
    }

    environment {
        MAVEN_HOME = tool name: 'Maven 3.9.8', type: 'maven' // Set MAVEN_HOME environment variable
        PATH = "${MAVEN_HOME}/bin:${env.PATH}" // Update PATH to include Maven binaries
    }

    stages {
        stage('Build') {
            agent {
                label 'cimg/openjdk:21.0.2-browsers' // Specify Docker image label for agent
            }
            steps {
                script {
                    // Run commands inside the Docker container
                    docker.image('cimg/openjdk:21.0.2-browsers').inside {
                        // Commands to run inside the Docker container
                        sh 'mvn -B -DskipTests clean package'
                    }
                }
            }
        }
        // Add more stages as needed
    }
}
