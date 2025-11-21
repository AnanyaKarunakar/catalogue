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
        stage{
            steps('Build'){
                echo 'Building'
            }
        }
        stage('Test'){
            steps{
                
            }
        }
        stage{
            steps{
                
            }
        }
    }
    post{
        always {

        }
        success {

        }
        failure {
            
        }
    }
}