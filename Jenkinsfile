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
      
      stage('Deploy Application on K8s') {
              steps
              {
                
                sshagent(['ssh-key']) {
    // some block
                       sh "scp -o StrictHostKeyChecking=no Node.yaml prabhat_1121485@13.93.120.161:/home/prabhat_1121485/"
                      script{
                        try{
                            sh "prabhat_1121485@13.93.120.161 kubectl apply -f ."
                        }catch(error){
                            sh "prabhat_1121485@13.93.120.161 kubectl create -f ."
                        }
                    }
}
               
    }
       }
  
  
  
  }
         }
