pipeline {
    agent any

    environment {
        // Définir les variables d'environnement, si nécessaire
    }

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code source du dépôt Git
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Ajouter des commandes pour construire votre projet
                sh 'pnpm install'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests
                sh 'pnpm dev'
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                script {
                    // Utiliser les identifiants stockés dans Jenkins
                    withCredentials([string(credentialsId: 'NETLIFY_TOKEN', variable: 'TOKEN')]) {
                        // Exemple de commande de déploiement pour Netlify
                        sh 'npm run build'
                        sh 'netlify deploy --prod --auth $TOKEN --dir ./build'
                    }
                    // Ou pour Vercel
                    // Remplacer 'VERCEL_TOKEN' par l'ID des identifiants de Vercel
                    // withCredentials([string(credentialsId: 'VERCEL_TOKEN', variable: 'TOKEN')]) {
                    //    sh 'vercel --token $TOKEN --prod'
                    // }
                }
            }
        }
    }

    post {
        always {
            // Actions à effectuer après les stages, comme le nettoyage
        }
        success {
            // Actions en cas de succès
        }
        failure {
            // Actions en cas d'échec
        }
    }
}
