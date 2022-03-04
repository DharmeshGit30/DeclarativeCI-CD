def mvn
pipeline {
  agent any
    tools {
      maven 'Maven3'
//      jdk 'JAVA_HOME'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('SonarCloud') { //Trigger SonarCloud to check Bugs and vilations 
            environment {
                SCANNER_HOME = tool 'SonarQubeScanner'
                ORGANIZATION = "dharmeshgit30"
                PROJECT_KEY = "DharmeshGit30_simple-java-maven-app"
            }
            steps {
              withSonarQubeEnv('Sonar-Cloud') {
                sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                -Dsonar.projectKey=$PROJECT_KEY  
                -Dsonar.java.binaries=target/classes/com/example/helloworld'''
              }
            }
        } 
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
//        stage('Deliver') {
//            steps {
//                sh './jenkins/scripts/deliver.sh'
//            }
//        }
    }
}
