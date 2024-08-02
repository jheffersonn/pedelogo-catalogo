pipeline{
    agent any

    stages{
        
        stage('Get Source'){
            echo 'Get Source...'
            steps{
                git url: 'https://github.com/jheffersonn/pedelogo-catalogo.git', branch: 'main'
            }
        }

        stage('Docker Build'){

            steps{
                script{
                    echo 'Docker Build...'
                    dockerapp = docker.build("jeffersondevops/pedelogo-catalogo:${env.BUILD_ID}",
                        '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
                
            }
        }

        stage('Docker Push Image'){
            
            steps{
                script{
                    echo 'Docker Push Image...'
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub' ){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")

                    }
                }
            }
        }

        stage('Deploy Kubernetes'){
            
            steps{
                echo 'Deploy Kubernetes...'
                withKubeConfig([credentialsId: 'kubeconfig']){
                    sh 'kubectl apply -f ./deployment.yaml'
                }
            }
        }

    }
}