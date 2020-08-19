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
                sh("curl -LO https://storage.googleapis.com/kubernetes-release/release/\$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl")
                sh("chmod +x ./kubectl")
                sshagent(['ssh-key']) {
    // some block
    sh("cat ./Node.yaml | ./kubectl apply -f -")
}
               
    }
       }
  
  
  
  }
         }
