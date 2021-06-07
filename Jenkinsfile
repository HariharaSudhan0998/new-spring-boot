  
pipeline {
   agent any

  stages {
     stage('Compile') {
     steps {
        sh(script: 'mvn compile')
        echo 'Compile...'
     }
   }
	  stage('Package') {
     steps {
        sh(script: 'mvn package')
        echo 'Package...'
     }
   }
	  stage('Artifact Push') {
     steps {	          	   
             sh(script: 'mvn deploy ')	    
        echo 'Artifact Push...'
     }
   }
    
     stage('Deploy to Production') {
       steps {	
	     script {
             sshagent (credentials:['productionserver']) { 
	     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.15 "killall -9 java; rm -rf gs-spring-boot-1.0.1.jar; ls -ltr; ps -ef |grep java ;wget http://65.1.231.149:8081/repository/docker-web-service/org/springframework/gs-spring-boot/1.0.1/gs-spring-boot-1.0.1.jar; "'	
	     sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.15 "sudo docker build -t test .;docker run -d -p 8080:8080 --name test;"'
	    // sh 'ssh -o StrictHostKeyChecking=no ec2-user@172.31.7.15 "pwd; ls -ltr; java -jar gs-spring-boot-1.0.1.jar 2>> /dev/null >> /dev/null &"; sleep 10; ps -ef |grep java'
   }
  }
				    
        echo 'Deploy to Production...'
     }
   } 
  }
}
