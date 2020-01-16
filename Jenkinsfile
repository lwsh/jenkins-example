pipeline {
    agent { docker { image 'maven:3.3.3' } }

    stages {
        stage ('Compile Stage') {

            steps {
                    sh 'mvn clean install'
            }
        }
        
        stage ('Deployment Stage') {
            steps {

                sh '/usr/local/bin/aws s3 cp target/jenkins-example*.jar s3://techprimers-s3/'
                sh '/usr/local/bin/aws s3 ls'
                sh '/usr/local/bin/aws s3 ls s3://techprimers-s3/'
            }
        }
    }
}