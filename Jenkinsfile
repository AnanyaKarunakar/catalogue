pipeline{
    agent {
        label 'AGENT'
    }
    environment {
        appVersion = ''
    }
    stages{
        stage('Read package.json'){
            steps {
                script {
	                def packageJson = readJSON file: 'package.json'
		            appVersion = packageJson.version
		            echo "package version: ${appVersion}"
                }
            }
        }
        stage('Build'){
            steps{
                echo 'Building'
            }
        }
        stage('Test'){
            steps{
                echo 'Testing'
            }
        }
        stage('Deploy'){
            steps{
                echo 'Deploying'
            }
        }
    }
    post{
        always {
            echo "Hello Always"
        }
        success {
            echo "Hello Success"
        }
        failure {
            echo "Hello Failure"
        }
    }
}