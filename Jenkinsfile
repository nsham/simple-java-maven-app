pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
//        stage('Test') {
//            steps {
//                sh 'mvn test'
//            }
//            post {
//                always {
//                    junit 'target/surefire-reports/*.xml'
//                }
//            }
//        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
//                    sh 'mvn -X org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
                    sh 'mvn -X clean package sonar:sonar'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
