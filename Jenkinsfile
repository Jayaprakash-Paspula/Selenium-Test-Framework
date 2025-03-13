pipeline { 
    agent any  

    tools {
        maven 'maven' 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hverma22/Selenium-Test-Framework.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Reports') {
            steps {
                publishHTML(target: [
                    reportDir: 'src/test/resources/ExtentReport',  
                    reportFiles: 'ExtentReport.html',  
                    reportName: 'Extent Spark Report'
                ])
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/src/test/resources/ExtentReport/*.html', fingerprint: true
            junit 'target/surefire-reports/*.xml'
        }
    }
}
