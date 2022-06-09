pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: ''https://github.com/swapmnew/CI-CD-using-Docker-master
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp/my-repo:latest .' 
                sh 'docker tag samplewebapp swapnilnew01/my-repo:latest'
                //sh 'docker tag samplewebapp swapnilnew01/my-repo:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push swapnilnew01/my-repo:latest'
        //  sh  'docker push swapnilnew01/my-repo:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 swapnilnew01/my-repo"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://jenkins@192.168.56.4 run -d -p 8003:8080 swapnilnew01/my-repo"
 
            }
        }
    }
	}
    
