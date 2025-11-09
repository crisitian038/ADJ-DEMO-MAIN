pipeline {
    agent any 

    stages {
        // Parar todos los servicios
        stage('parando los servicios') {
            steps {
                bat '''
                docker compose -p adj-demo-c down 
                '''
            }
        }
        
        // Eliminar las imágenes anteriores
        stage('borrando imagenes antiguas') {
            steps {
                bat '''
                FOR /F "tokens=*" %%i IN ('docker images --filter "label=com.docker.compose.project=adj-demo-c" -q') DO (
                    docker rmi %%i
                )
                IF ERRORLEVEL 1 (
                    echo no hay imagenes para borrar
                )
                '''
            }
        }
        
        // Bajar actualizaciones
        stage('actualizando codigo') {
            steps {
                checkout scm
            }
        }
        
        // Levantar y desplegar el proyecto
        stage('construyendo y desplegando') {
            steps {
                bat '''
                docker compose up --build -d
                '''
            }
        }
    }
    
    post {
        success {
            echo 'proceso ejecutado con exito'
        }
        failure {
            echo 'error al ejecutar el pipeline'
        }
        always {
            echo 'fin del pipeline'
        }
    }
}
