pipeline {
    agent any
    tools {
        maven 'Maven3'
 jdk 'JAVA11'
    }
    stages {
        stage("Tools initialization") {
            tools {
                   jdk "JAVA11"
                }
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                git branch: 'main',
                url: "https://github.com/devops81/webapp1.git"
            }
        }
        stage("Building Application") {
            steps {
               sh "mvn clean install"
            }
            }
            
      /*  stage("JUNIT REPORT") {
            steps {
               junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
            }
        } */
        
           
    stage ('Scan and Build Jar File') {
            steps {
               withSonarQubeEnv(installationName: 'sonarqubeserver', credentialsId: 'sonarqube-token') {
                sh 'mvn clean package sonar:sonar'
                }
            }
        }
        }

           post {
        always {
            
            junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
            
        }
        }
           
        
        }
