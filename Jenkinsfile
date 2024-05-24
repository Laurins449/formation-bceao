pipeline {
    agent any

   

    stages {
               
        stage('build artefact') {
            steps {
               sh 'mvn clean package -DskipTests '
            }

           
        }
        
         stage('test') {
            steps {
               sh 'mvn test'
            }

           
        }
        
       stage('buld and push image') {
            steps {
                
                withDockerRegistry([credentialsId: "my-jenkins-docker-hub", url: ""]) {
                     sh 'printenv'
                     sh 'docker build -t docker449/demo-boot-jenkins:$BUILD_NUMBER .'
                     sh 'docker push  docker449/demo-boot-jenkins:$BUILD_NUMBER'
                }
              
            }

           
        }
        
        stage('start application') {
            when { expression { false } }
            steps {
               sh 'docker stop instance-demo-bceao || true '
               sh 'docker rm instance-demo-bceao || true '
               sh 'docker run -d -p 8180:8180 --name instance-demo-bceao demo-boot-jenkins '
            }

           
        }
    }
}
