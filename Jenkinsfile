pipeline {
  agent any 
  tools {
    maven 'Maven'
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
    
      stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/Azraguid/webapp.git > trufflehog'
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
                           sh 'scp -i /home/ubuntu/aws.pem -o StrictHostKeyChecking=no target/*.war ubuntu@3.15.176.132:/home/ubuntu/apache-tomcat-8.5.47/webapps/webapp.war'
                    
           }       
    }
    

    
   
  }
}
