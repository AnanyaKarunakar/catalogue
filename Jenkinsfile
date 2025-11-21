pipeline{
    agent {
        label 'AGENT'
    }
    environment {
        appVersion = ''
        REGION = 'us-east-1'
        ACC_ID = '277789128698'
        PROJECT = 'roboshop'
        COMPONENT = 'catalogue'
    }
    stages{
        stage('Read package.json '){
            steps {
                script {
	                def packageJson = readJSON file: 'package.json'
		            appVersion = packageJson.version
		            echo "package version: ${appVersion}"
                }
            }
        }
        stage('Install Dependices '){
            steps{
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        // stage('Docker Build & Push') {
        //     steps {
        //         script {
        //             withAWS(region: 'us-east-1', credentials: 'AWS-CREDENTIAL-ID') {
        //                     sh '''
        //                         aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 277789128698.dkr.ecr.us-east-1.amazonaws.com

        //                         docker build -t 277789128698.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion} .
                            
        //                         docker push 277789128698.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:${appVersion}
        //                     '''
        //             }
        //         }
        //     }
        // }

        stage('Docker Build'){
            steps{
                script{
                   withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                        sh """
                            aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 277789128698.dkr.ecr.us-east-1.amazonaws.com

                            docker build -t 277789128698.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:1.0.0 .

                            docker push 277789128698.dkr.ecr.us-east-1.amazonaws.com/roboshop/catalogue:1.0.0

                        """
                   } 
                }
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