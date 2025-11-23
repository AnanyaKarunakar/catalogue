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

        stage('Docker Build'){
            steps{
                script{
                   withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                        sh """
                            # Delete all existing images to ensure only one version stays
                            aws ecr list-images \
                            --repository-name ${PROJECT}/${COMPONENT} \
                            --region ${REGION} \
                            --query 'imageIds[*]' \
                            --output json | \
                            aws ecr batch-delete-image \
                            --repository-name ${PROJECT}/${COMPONENT} \
                            --image-ids file:///dev/stdin \
                            --region ${REGION} || true
                        """

                        sh """
                            aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com

                            docker build -t ${ACC_ID}.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion} .

                            docker push 277789128698.dkr.ecr.${REGION}.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}

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