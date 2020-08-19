pipeline {
       agent any
       environment {
   registry = "prabhat2020/nodecal"
   registryCredential = "06216ef3-ad77-49a6-a37b-e2e91cd08bfb"
  }
  stages {
  
  stage('Building our image') { 
             steps { 
                    script {
                 dockerImage = docker.build registry 
                    }
                 } 

     }
     
     stage('Deploy our image') { 
          steps { 
                 script { 
                  docker.withRegistry( '', registryCredential ) { 
                  dockerImage.push() 
                        }
                   } 
          }
      }
      
      stage("Deploy on AKS using cluster"){
              steps { 
    	            def kubeCMD = 'kubectl apply -f Node.yaml -n prabhat'
    	            sshagent(['prabhat_1121485']){
    	            sh 'ssh -o StrictHostKeyChecking=no prabhat_1121485@13.93.120.161 ${kubeCMD}'
                   }
    	}
    }
  
  
  }
         }
