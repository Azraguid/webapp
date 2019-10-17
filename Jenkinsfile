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
    
        stage ('Source Composition Analysis') {
      steps {
         sh 'rm owasp* || true'
         sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         sh 'chmod +x owasp-dependency-check.sh'
         sh 'bash owasp-dependency-check.sh'
         sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
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
