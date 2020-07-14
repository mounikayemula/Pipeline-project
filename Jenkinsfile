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
            scp -o StrictHostKeyChecking=no  target/*.war ec2-user@ec2-34-219-104-198.us-west-2.compute.amazonaws.com:/opt/tomcat8/webapps/
            ssh ec2-user@ec2-34-219-104-198.us-west-2.compute.amazonaws.com /opt/tomcat8/bin/shutdown.sh
            ssh ec2-user@ec2-34-219-104-198.us-west-2.compute.amazonaws.com /opt/tomcat8/bin/startup.sh
            
            """
              }
            }
        }
    }
}

