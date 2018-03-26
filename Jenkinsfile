pipeline {
  agent any

  tools {
    maven 'mvn-3.5.2'
  }

  stages {
    stage('Maven Build') {
      steps {
        sh 'mvn package'
      }
    }
    
    stage('Docker Build') {
      steps {
      sh "docker build -t caprearch/helloworld-war:${env.BUILD_ID} ."
      sh "docker tag caprearch/helloworld-war:${env.BUILD_ID} caprearch/helloworld-war:latest"
      }
    }
	
	stage("init") {
      steps {
        withCredentials([usernamePassword(
          credentialsId: "docker",
          usernameVariable: "caprearch",
          passwordVariable: "caprearch"
        )]) {
          sh "docker login -u $USER -p $PASS"
		  sh 'docker push caprearch/helloworld-war:${env.BUILD_ID}'
        }
      }
    }
	
   } 
  }
  
  
  
  
/////feature/////
  
  
  //  stage('Check Specification') {
  //    steps {
   //     sh "chmod o+w *"
   //     sh "docker-compose up --exit-code-from cucumber --build"
   //   }
   // }
 // }

 // post {
 //   always {
 //     archive 'target/**/*.jar'
 //     junit 'target/**/*.xml'
 //     cucumber '**/*.json'
 //   }
 // }
//}
  //  success {
  //    withCredentials([usernamePassword(credentialsId: 'docker-credentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
  //      sh "docker login -u ${USERNAME} -p ${PASSWORD}"
  //      sh "docker push naresh/helloworld-war:${env.BUILD_ID}"
  //      sh "docker push naresh/helloworld-war:latest"
  //    }
   // }
 // }
//}