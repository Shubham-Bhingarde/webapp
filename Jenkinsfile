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
//        stage ('Deploy-To-Tomcat') {
//            steps {
//          sshagent(['tomcat']) {
//                sh 'scp -v -o StrictHostKeyChecking=no target/*.war shubham@192.168.52.128:/home/shubham/prod/apache-tomcat-8.5.78/webapps/webapp.war'
//             }      
//           }       
//    }
     stage ('SCAN for DAST') {
     steps {
     sh 'sudo docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-baseline.py -t http://192.168.52.128:8080/WebApp -r /home/shubham/report.html'
       }
   }
    }
 }
