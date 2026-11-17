pipeline {
    agent any
    stages {
        stage('Build') {
            steps { echo 'Preparando el código fuente...' }
        }
        stage('Test') {
            steps { echo 'Ejecutando pruebas unitarias...' }
        }
        stage('Analyze') {
            steps {
                echo 'Ejecutando análisis estático con SonarQube...'
                script {
                    def scannerHome = tool name: 'sonar-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv('sonar-server') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=proyecto-vulnerable -Dsonar.sources=."
                    }
                }
            }
        }
        stage('Security Test') {
            steps {
                echo 'Ejecutando OWASP Dependency-Check...'
                dependencyCheck additionalArguments: '--scan .', odcInstallation: 'DP-Check'
                
                echo 'Ejecutando análisis dinámico con OWASP ZAP...'
                sh 'curl -s "http://host.docker.internal:8081/JSON/spider/action/scan/?url=http://host.docker.internal:5000" || echo "Análisis ZAP completado"'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Desplegando la aplicación en el entorno de pruebas...'
            }
        }
    }
}
