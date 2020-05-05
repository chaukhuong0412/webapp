pipeline {
  agent any 
  stages {
    
    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/chaukhuong0412/webapp.git > trufflehog'
        sh 'cat trufflehog'
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
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.139.83.33:/prod/apache-tomcat-8.5.54/webapps/webapp.war'
              }      
           }       
    }
   
    
    
    
  }
}
