pipeline { 
    environment { 
        registry = "ezzathassan/newrepo1" 
        registryCredential = 'Dockerhub' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Clone Git') { 
            steps { 
                git 'https://github.com/ezzat09/BakeHouse' 
            }
        } 
        stage('Building new image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
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
        stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
    }
    }

