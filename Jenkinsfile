pipeline {
    agent { label 'master' }
    stages {
        stage('Clone sources') {
            steps {
                git branch: 'frature/mycode', credentialsId: 'neerajpawar2', url: 'https://github.com/neerajpawar2/helloworldapps.git'
            }
        }
		
		stage('Delete artifacts') {
            steps {
                sh "rm -fr ${WORKSPACE}/target"
            }
        }
       

        stage ("Maven Build") {
          environment {
            MAVEN_HOME = tool 'maven3.6' // this is the name of maven configured on global configuration tool
          }        
          steps {
             configFileProvider([configFile(fileId: '63c432ef-319d-43e1-9383-d38fd8bea6ad', variable: 'MAVEN_SETTINGS_XML')]) {
             tool name: 'maven3.6', type: 'maven'
             sh "${MAVEN_HOME}/bin/mvn -s $MAVEN_SETTINGS_XML install clean deploy"
             } 
          }     
              
        }
		
		stage('list artifacts') {
            steps {
			    sh "ls -ltr ${WORKSPACE}"
                sh "ls -ltr ${WORKSPACE}/target"
            }
        }
               
 
		stage('deploy artifacts') {
            steps {
			    sh "cp ${WORKSPACE}/target/helloworldapps-1.0-SNAPSHOT.war /root/apps/tomcat/package/apache-tomcat-9.0.65/webapps/helloworldapp.war"
                sh "ls -ltr /root/apps/tomcat/package/apache-tomcat-9.0.65/webapps"
            }
        }        
     
        
    }
}