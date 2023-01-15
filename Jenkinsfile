pipeline {
  agent any 
  tools {
    maven 'maven'
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


   
    stage ('Deploy to Tomcat') {
      steps {
        sshagent(['root']){
            sh 'tomcat -p "tomcat" scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/webapp-cicd-pipeline/target/WebApp.war root@192.168.11.16:/root/prod/apache-tomcat-9.0.71/webapps/webapp.war'    
        
        }
       }
    }



    }
}
