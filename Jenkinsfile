pipeline {
    agent any
   
    stages {

        stage('Run Selenium Tests with pytest') {
            steps {
                    echo "Running Selenium Tests using pytest"


                    bat 'pip install -r requirements.txt'


                    bat 'start /B python app.py'


                    bat 'ping 127.0.0.1 -n 5 > nul'

                    
                    bat 'python -m pytest -v'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t mypythonapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u gayathri3123 -p gayathri-3G'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag mypythonapp:v1 gayathri3123/devopsexam_repository:mypythonappimage"               
                    
                bat "docker push gayathri3123/devopsexam_repository:mypythonappimage"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}