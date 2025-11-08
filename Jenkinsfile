pipeline {
    agent any 

    stages {
        //parar todos los sevicios
        stage('parando los servicios'){
            steps{
                sh '''
                docker compose -p adj-demo-c down 
                 '''
            }
        }
        //eliminar las imagenes anteriores
        stage('parando los servicios'){

        }
        //eliminar las imagenes anteriores
        stage('borrando imaganes antiguas'){
            steps{
                sh '''
                IMAGES= $(docker images --filter "label= com.docker.compose.project=adj-demo-c" -q)
                if [ -n "$IMAGES" ]; then
                    dockerimages rmin $IMAGES
                    else
                    echo "no hay imagenes para borrar"
                    fi
                 '''
            }
        }
        //bajar actualizaciones
        stage('actualizando '){
            steps{
                checkout scm
            }
        }
        //levantar y desplegar el proyecto
         stage('construyendp y desplegando...'){
            sh '''
                docker compose up --build -d
                 '''
        }
    }
    post{
        success{
            echo 'proceso ejecutado con exito'
        }
        failure{
            echo'error al ejecutar el pipeline'
        }
        always{
            echo 'fin del pipeline'
        }
    }
}