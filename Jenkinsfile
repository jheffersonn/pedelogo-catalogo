pipeline{
    agent any

    stages{
        
        stage('Get Source'){
            steps{
                git url: 'https://github.com/jheffersonn/pedelogo-catalogo.git', branch: 'main'
            }
        }

        stage('Docker Build'){
            steps{
                script{
                    dockerapp = docker.build("jeffersondevops/pedelogo-catalogo:${env.BUILD_ID}",
                        '-f ./src/PedeLogo.Catalogo.Api/Dockerfile .')
                }
                
            }
        }
    }
}