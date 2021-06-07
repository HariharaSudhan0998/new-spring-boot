  
pipeline {
   agent any

  stages {
     stage('Compile') {
     steps {
        sh(script: 'mvn compile')
        echo 'Compile...'
     }
   }
    stage('Unit Test') {
     steps {
        sh(script: 'mvn test -Dtest=!SeleniumTest ')	    
	//sh(script: 'mvn package')
	 junit 'target/surefire-reports/*.xml'
        echo 'Unit Test...'
     }
   } 
  /*  stage('Code Quality') {
     steps {	    	    
           withSonarQubeEnv('sonarqube') {
		     sh """ 		        
                       mvn sonar:sonar \
                      -Dsonar.projectKey=sonar \
                      -Dsonar.host.url=http://65.2.108.33:9000 \
                         
                       """ 
		        } 
        
        echo 'Code Quality...'
	}
   }
    stage('Artifact Push') {
     steps {	          
	   //  sh(script: 'mvn  -version')-Dtest=!SeleniumTest
             sh(script: 'mvn deploy -Dtest=!SeleniumTest')
	    // sh(script:'mvn clean package -Drevision=01')
        echo 'Artifact Push...'
     }
   }
   stage('Deploy to Test') {
	      steps{
		      
		   script {
               sshagent (credentials:['deployserver']) { 
                sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.9.220 "killall -9 java; rm -rf gs-spring-boot-1.0.2.jar; ls -ltr; ps -ef |grep java; wget http://65.1.231.149:8081/repository/spring-boot/org/springframework/gs-spring-boot/1.0.2/gs-spring-boot-1.0.2.jar; "'		
                sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.9.220 "pwd; ls -ltr; java -jar gs-spring-boot-1.0.2.jar 2>> /dev/null >> /dev/null &"; sleep 10; ps -ef |grep java'
		   }                 
	      } 
		       	  
                       echo 'Deploy to dev...'
        }
   }
     stage('Functional Test') {
     steps {       		   
	    //  sh('mvn install -Dmaven.test.skip=true')
	      sh(' mvn test -Dtest=SeleniumTest ')
	    // -Dtest=SeleniumTest
        echo 'Functional Test...'
		     }
   } 
     stage('Deploy to Production') {
       steps {	
	     script {
             sshagent (credentials:['productionserver']) { 
	     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.15 "killall -9 java; rm -rf gs-spring-boot-1.0.2.jar; ls -ltr; ps -ef |grep java ; wget http://65.1.231.149:8081/repository/spring-boot/org/springframework/gs-spring-boot/1.0.2/gs-spring-boot-1.0.2.jar;"'		
	     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.15 "pwd; ls -ltr; java -jar gs-spring-boot-1.0.2.jar 2>> /dev/null >> /dev/null &"; sleep 10; ps -ef |grep java'
   }
  }
				    
        echo 'Deploy to Production...'
     }
   }  
      stage('Smoke Test') {
      steps {       			     
	    sh ('curl http://65.1.231.149:8080')
        echo 'Smoke Test...'
		     }
   } */
  }
}
