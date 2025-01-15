pipeline {
    agent any
    
    environment {
        PYTHON_VERSION = '3.9'
        NODE_VERSION = '20'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Cloner le dépôt React
                dir('react-app') {
                    git 'https://github.com/bonitoFotso/DocGen.git'
                }
                // Cloner le dépôt Django
                dir('django-app') {
                    git 'https://github.com/bonitoFotso/KES_DocGen.git'
                }
            }
        }
        
        stage('Build React App') {
            steps {
                dir('react-app') {
                    nodejs(nodeJSInstallationName: "Node ${NODE_VERSION}") {
                        sh 'npm install'
                        sh 'npm run build'
                    }
                }
            }
        }
        
        // stage('Test React App') {
        //     steps {
        //         dir('react-app') {
        //             nodejs(nodeJSInstallationName: "Node ${NODE_VERSION}") {
        //                 sh 'npm test'
        //             }
        //         }
        //     }
        // }
        
        stage('Build Django App') {
            steps {
                dir('django-app') {
                    withPythonEnv("python${PYTHON_VERSION}") {
                        sh 'pip install -r requirements.txt'
                        sh 'python manage.py migrate'
                    }
                }
            }
        }
        
        // stage('Test Django App') {
        //     steps {
        //         dir('django-app') {
        //             withPythonEnv("python${PYTHON_VERSION}") {
        //                 sh 'python manage.py test'
        //             }
        //         }
        //     }
        // }
    }
    
    post {
        always {
            cleanWs()
        }
        success {
            echo 'Le pipeline a réussi !'
        }
        failure {
            echo 'Le pipeline a échoué.'
        }
    }
}