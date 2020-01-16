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

        stage('Generate HTML report') {
            steps {
                cucumber buildStatus: "UNSTABLE",
                        fileIncludePattern: '**/cucumber.json',
                        jsonReportDirectory: 'target'
            }

        }
    }
}