pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'M3'
    }

    triggers {
        githubPush()
    }

    stages {
        stage('Récupération du projet') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-creds',
                    url: 'https://github.com/AmineBouchnatEsprit/DevOps.git'
            }
        }

        stage('Génération du livrable') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
        }
    }
}
