pipeline {
    agent { docker { image 'maven:3.3.3' } }

    stages {
        stage ('Compile Stage') {

            steps {
                    sh 'mvn clean compile'
            }
        }

        stage ('Testing Stage') {

            steps {
                    sh 'mvn test'
            }
        }

        stage('Sonarqube') {
            def scannerHome = tool 'SonarScanner 4.0'

            steps {
                withSonarQubeEnv('sonarqube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                }

                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }


        stage ('Deployment Stage') {
            steps {
                    sh 'mvn deploy'
            }
        }
    }
}