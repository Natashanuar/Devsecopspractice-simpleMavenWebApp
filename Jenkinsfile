pipeline {
  agent any 
    tools {
      maven 'Maven'
  }
  
  stages {
    stage ('Initialize') {
      steps {
        /*sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' */
           echo 'initialize'
      }
    }
    
    
   stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
    
    stage ('Software Composition Analysis') {
      steps {
         //echo 'SCA'
         sh 'rm -r dependency-check* || true' 
         sh 'wget https://github.com/jeremylong/DependencyCheck/releases/download/v6.0.3/dependency-check-6.0.3-release.zip'
         sh 'unzip dependency-check-6.0.3-release.zip'
         sh './dependency-check/bin/dependency-check.sh --scan ./* --enableRetired -f "ALL" '
       }
    }
    
    
     stage ('Deploy-To-Tomcat') {
            steps {
           /*sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@10.0.2.15:/home/ubuntu/prod/apache-tomcat-8.5.61/webapps/webapp.war'
              }*/
             echo 'Tomcat'
           }      
    }  
  } 
}
