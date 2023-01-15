pipeline {
    agent any
  
     //create dockerhub credential in github with your dockerhub Username and Password/Token
    environment {
      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/adeoyedewale/Backend.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                //sh 'npm run build'
            }
        }
	    
        stage('Dockerize') {
            steps {
                sh "docker build -t eruobodo/mybackend-nodejs-app:${BUILD_NUMBER} ."
            }
        }
        stage('Publish') {
            steps {
                sh "docker login -u eruobodo -p Fifehanmi@2021"
                sh "docker tag mybackend-nodejs-app:$BUILD_NUMBER eruobodo/mybackend-nodejs-app:$BUILD_NUMBER"
                sh "docker push eruobodo/mybackend-nodejs-app:$BUILD_NUMBER"
            }
        //stage('Login') {
		
              //steps {
              //   sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username eruobodo --password-stdin'    
             // }
		   // }

        //stage('Push') {

             // steps {
                 //sh 'docker push eruobodo/backend-app:${BUILD_NUMBER}'
             // }
       // }
		}
	}
	
    post {
        always {
	cleanWs()
      	sh 'docker logout'
        }
   }
}
