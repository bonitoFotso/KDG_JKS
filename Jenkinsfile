pipeline {
    agent any
    
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
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        
       // stage('Test React App') {
       //     steps {
       //         dir('react-app') {
       //             sh 'npm test'
       //         }
       //     }
       // }
        
        stage('Build Django App') {
            steps {
                dir('django-app') {
                    sh 'pip install -r requirements.txt'
                    sh 'python manage.py migrate'
                }
            }
        }
        
        //stage('Test Django App') {
        //    steps {
        //        dir('django-app') {
        //            sh 'python manage.py test'
        //        }
        //    }
        //}
        
        stage('Deploy') {
            steps {
                // Ajoutez ici vos étapes de déploiement pour les deux applications
                sh 'echo "Déploiement effectué"'
            }
        }
    }
}
