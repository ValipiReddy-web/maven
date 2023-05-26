pipeline {
  agent any 
  
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
        sh 'docker run gesellix/trufflehog --json https://github.com/ValipiReddy-web/maven.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    
    stage ('Source Composition Analysis') {
      steps {
         //sh 'rm owasp* || true'
         //sh 'wget "https://raw.githubusercontent.com/cehkunal/webapp/master/owasp-dependency-check.sh" '
         //sh 'chmod +x owasp-dependency-check.sh'
         //sh 'bash /var/lib/jenkins/owasp-dependency-check.sh'
          echo "This is pass check "
       //  sh 'cat /var/lib/jenkins/workspace/data/OWASP-Dependency-Check/reports/dependency-check-report.xml'
        
      }
    }
    
    stage ('SAST') {
      steps {
        //withSonarQubeEnv('sonar') {
          //sh 'docker run -d --name sonarqube -p 9000:9000 sonarqube'
          //sh 'mvn sonar:sonar'
          echo "sonar"
          //sh 'cat target/sonar/report-task.txt'
        //}
      }
    }
    
    stage ('Build') {
      steps {
      sh 'mvn clean install'
       }
    }
    
    stage ('Deploy-To-Tomcat') {
            steps {
              sh "cp -rf /var/lib/jenkins/workspace/dast/target/saigurus.war  /var/lib/jenkins/apache-tomcat-9.0.75/webapps"
           //sshagent(['tomcat']) {
                
             // }      
           }       
    }
    
    
    stage ('DAST') {
      steps {
        sh 'docker run -t owasp/zap2docker-stable zap-baseline.py -t http://104.198.246.144/:9090/saigurus/'
        //sshagent(['zap']) {
         //sh 'docker run -t owasp/zap2docker-stable zap-baseline.py -t http://13.232.202.25:8080/webapp/" || true'
        //}
      }
    }
    
  }
}
