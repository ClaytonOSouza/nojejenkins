pipeline {
   environment {
     dockerRegistry = "claytondevops/nodejenkins"
     dockerRegistryCredential = 'Almerita@040876$#@'
     dockerImage = ''
   }
   agent any
   tools {node "node" }
   stages {
     stage('Cloning Git') {
       steps {
         git 'https://github.com/ClaytonOSouza/nojejenkins.git'
       }
     }
     stage('Build') {
        steps {
          sh 'npm install'
        }
     }
     stage('Test') {
       steps {
         sh 'npm test'
       }
     }
     stage('Building image') {
       steps{
         script {
           dockerImage = docker.build dockerRegistry + ":$BUILD_NUMBER"
         }
       }
     }
     stage('Upload Image') {
       steps{
         script {
           docker.withRegistry( '', dockerRegistryCredential ) {
             dockerImage.push()
           }
         }
       }
     }
     stage('Remove Unused docker image') {
       steps{
         sh "docker rmi $dockerRegistry:$BUILD_NUMBER"
       }
     }
   }
 }

