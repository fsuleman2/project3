pipeline {
    agent any 
    stages {
        stage('Compile and Clean') { 
            steps {

                sh "mvn clean compile"
            }
        }
        stage('build') { 
            steps {
                bat "mvn package"
            }
        }
        stage('Build Docker image'){
            steps {
              
                bat 'docker build -t  fsuleman2/revature-railways-backend .'
            }
        }
        stage('Docker Login'){
            
            steps {
                withCredentials([string(credentialsId: 'fsuleman2', variable: 'Dockerpwd')]) {
    sh "docker login -u fsuleman2 -p ${Dockerpwd}"
}
             
            }                
        }
        stage('Docker Push'){
            steps {
                bat 'docker push fsuleman2/revature-railways-backend'
            }
        }
        stage('Docker deploy'){
            steps {
              bat 'docker container rm -f revature-railways-backend'
                bat 'docker run --name revature-railways-backend -itd -p  9090:9848 fsuleman2/revature-railways-backend'
            }
        }        
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}
