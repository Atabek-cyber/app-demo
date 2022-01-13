pipeline {
    agent any 
    environment {
        //once you sign up for Docker hub, use that user_id here
        registry = "atabekcyber/dockertest"
        //- update your credentials ID after creating credentials for connecting to Docker Hub
        registryCredential = 'dockerHub'
        dockerImage = ''
    }
    
    stages {
        stage('Cloning Git') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/Atabek-cyber/app-demo.git']]])       
            }
        }
    stage('Docker ps') {
      steps{
        script {
          /bin/bash "docker ps"
        }
      }
    }
    // Building Docker images
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry
        }
      }
    }

         // Uploading Docker images into Docker Hub
    stage('Uploading Image') {
     steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
            }
        }
      }
    }
    
//      // Stopping Docker containers for cleaner Docker run
//      stage('docker stop container') {
//          steps {
//             sh 'docker ps -f name=mypythonappContainer -q | xargs --no-run-if-empty docker container stop'
//             sh 'docker container ls -a -fname=mypythonappContainer -q | xargs -r docker container rm'
//          }
//        }
    
    
//     // Running Docker container, make sure port 8096 is opened in 
//     stage('Docker Run') {
//      steps{
//          script {
//             dockerImage.run("-p 8096:5000 --rm --name mypythonappContainer")
//          }
//       }
//     }
    }
}
