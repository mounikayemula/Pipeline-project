pipeline {
    agent any
  tools {
    maven 'M2_HOME'
    }
    stages {
        stage('---clean---') {
            steps {
                sh "mvn clean"
            }
        }
        stage('--test--') {
            steps {
                sh "mvn test"
            }
        }
        stage('--package--') {
            steps {
                sh "mvn package"
            }
        }
       stage("deploy-ec2"){
            steps{
            sshagent(['dev-server']) {
            sh """
            scp -o StrictHostKeyChecking=no  target/myapp.jar ec2-user@ec2-35-165-98-58.us-west-2.compute.amazonaws.com:/opt/tomcat8/webapps/
            ssh ec2-user@ec2-35-165-98-58.us-west-2.compute.amazonaws.com /opt/tomcat8/bin/shutdown.sh
            ssh ec2-user@ec2-35-165-98-58.us-west-2.compute.amazonaws.com /opt/tomcat8/bin/startup.sh
            
            """
              }
            }
        }
    }
