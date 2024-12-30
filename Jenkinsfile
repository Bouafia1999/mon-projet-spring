pipeline {
    agent any  // Utilise n'importe quel agent disponible (local ici)

    stages {
        stage('Cloner le dépôt') {
            steps {
                // Clone le dépôt Git depuis GitHub
                git url: 'https://github.com/Bouafia1999/mon-projet-spring.git'
            }
        }

        stage('Build du projet') {
            steps {
                script {
                    // Exécuter le build avec Maven pour créer le fichier .jar
                    sh './mvnw clean package'
                }
            }
        }

        stage('Tests') {
            steps {
                script {
                    // Exécuter les tests Maven (unitaires, intégration, etc.)
                    sh './mvnw test'
                }
            }
        }

        stage('Déploiement local') {
            steps {
                script {
                    // Supprimer toute ancienne instance de l'application si nécessaire
                    sh 'taskkill /F /IM java.exe'

                    // Lancer l'application Spring Boot sur la machine locale
                    sh 'java -jar target/mon-projet-spring.jar'
                }
            }
        }
    }

    post {
        success {
            // Action à réaliser après un build réussi (par exemple, notifier ou archiver des fichiers)
            echo 'Le build a réussi, l\'application est déployée localement !'
        }
        failure {
            // Action à réaliser après un échec
            echo 'Le build a échoué.'
        }
    }
}
