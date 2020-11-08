pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
         stage('Archiveartifact') {
             steps {
                  archiveArtifacts artifacts: 'target/*.war'
             }
         }
                 stage ('Copy .war file to tomcat') {
             steps {
                 sh '''
                       sudo cp $WORKSPACE/target/*.war /opt/tomcat/tomcat9/webapps/
                    '''
             }
         }
        stage ('Restarting application') {
             steps {
                 sh '''
                      /opt/tomcat/tomcat9/bin/catalina.sh start
                       systemctl stop tomcat
                       systemctl start tomcat
                       systemctl status tomcat
                    '''
             }
         }
    }
}
