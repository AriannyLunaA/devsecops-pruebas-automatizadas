pipeline {
    agent any
    stages {
        stage('Build') {
            steps { echo 'Preparando el código...' }
        }
        stage('Test') {
            steps { echo 'Ejecutando pruebas unitarias...' }
        }
        stage('Analyze') {
            steps { echo 'Análisis estático con SonarQube...' }
        }
        stage('Security Test') {
            steps { echo 'Ejecutando OWASP Dependency-Check y ZAP...' }
        }
        stage('Deploy') {
            steps { echo 'Desplegando la aplicación...' }
        }
    }
}
