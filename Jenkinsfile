pipeline {
    agent any
    tools {
       maven "M2_HOME"
    }
 }
    environment {
    registry = "nguelewie100/myapp"
    registryCredential = 'registryID'
    }
    stages {
        stage('Clone sources') {
            steps {
                git url: "<code here>"
            }
        }

        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./mvn sonarqube"
                }
            }
        }
        stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    stages {
      stage ('build') {
        steps {
       sh "mvn clean"
       sh "mvn install"
       sh "mvn package"
        }
      
      }
      
      stage ('test') {
        steps {
         echo "test step"
        sh "mvn test"
        
        }
      
      }
      
      stage ('deploy') {
        steps {
          script {
        docker.build registry + ":$BUILD_NUMBER"
        }
      
        }
      
      }
    
    }
 } 

