pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        bat '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
     stage ('Build') {
       steps {
      bat 'mvn clean package'
       }
       }
    
     stage ('Deploy-To-Tomcat') {
            steps {
                           bat 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@3.15.176.132:/home/ubuntu/apache-tomcat-8.5.47/webapps/webapp.war'
                    
           }       
    }
    
   
  }
}
