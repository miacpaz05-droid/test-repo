pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git 'git@github.com:miacpaz05-droid/test-repo.git'
            }
        }

        stage('Build JAR') {
            steps {
                sh 'echo dummy jar content > app.jar'
            }
        }

        stage('Upload to Nexus') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'nexus-creds',
                    usernameVariable: 'USERNAME',
                    passwordVariable: 'PASSWORD'
                )]) {
                    sh '''
                    curl -v -u $USERNAME:$PASSWORD \
                    --upload-file app.jar \
                    http://nexus:8081/repository/maven-releases/com/example/app/1.0/app-1.0.jar
                    '''
                }
            }
        }

        stage('Verify') {
            steps {
                sh 'ls -l'
            }
        }
    }
}
