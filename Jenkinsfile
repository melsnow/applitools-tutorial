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






/*pipeline {
    agent none // Use 'none' since we will specify agent in stages

    tools {
        maven 'Maven 3.9.8' // Define Maven tool installation
    }

    environment {
        MAVEN_HOME = tool name: 'Maven 3.9.8', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'cimg/openjdk:21.0.2-browsers'
                    args '-u root' // Optional: Run as root user
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        // Add more stages as needed
    }
}*/

pipeline {
    agent none // Define 'none' as we'll specify agent in each stage

    environment {
        MAVEN_HOME = tool name: 'Maven 3.9.8', type: 'maven'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'cimg/openjdk:21.0.2-browsers'
                    args '-u root' // Optional: Run as root user
                }
            }
            steps {
                script {
                    // Run Maven build commands inside Docker container
                    docker.image('cimg/openjdk:21.0.2-browsers').inside {
                        sh 'mvn -B -DskipTests clean package'
                    }
                }
            }
        }
        // Add more stages as needed
    }
}
