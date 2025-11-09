pipeline {
    agent any 

    stages {
        // Parar todos los servicios
        stage('parando los servicios') {
            steps {
                sh '''
                docker compose -p adj-demo-c down 
                '''
            }
        }
        
        // Eliminar las imágenes anteriores
        stage('borrando imagenes antiguas') {
            steps {
                sh '''
                IMAGES=$(docker images --filter "label=com.docker.compose.project=adj-demo-c" -q)
                if [ -n "$IMAGES" ]; then
                    docker rmi $IMAGES
                else
                    echo "no hay imagenes para borrar"
                fi
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
                sh '''
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
