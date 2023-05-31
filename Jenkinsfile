pipeline {
  agent any 
  tools {
    maven 'MAVEN'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
   stage ('Build') {
     steps {
     sh 'mvn clean package'
       }
   }
        stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war shubham@192.168.52.128:/var/lib/tomcat9/webapps/ROOT/webapp.war'
              }      
           }       
    }
    }
 }
