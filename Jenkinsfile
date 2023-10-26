pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the code from the GitHub repository
                checkout scm
            }
        }
        
         stage('back') {
            steps {
                // Zip the code in the current directory
                sh 'cd ..  '
            }
        } 
	  stage('list all') {
            steps {
                // Zip the code in the current directory
                sh 'ls'
            }
        }
        stage('Zip Code') {
            steps {
                // Zip the code in the current directory
                sh 'zip -r moodle_app.zip .'
            }
        }

        stage('Upload to GCR') {
            steps {
                // Use GCP credentials to upload the code to GCR
                withCredentials([file(credentialsId: 'gcp-credentials.json', variable: 'GCP_CREDENTIALS')]) {
                    sh 'gsutil cp moodle_app.zip gs://your-gcr-bucket/moodle_app.zip'
                }
            }
        }

        stage('Deploy to VM') {
            steps {
                // Use SSH credentials to connect to the VM
                sshagent(['your-ssh-credentials']) {
                    script {
                        sh '''
                            # SSH into your VM
                            ssh user@your-vm-ip

                            # Download and unzip the code from GCR
                            gsutil cp gs://your-gcr-bucket/moodle_app.zip /path/to/vm/directory/
                            unzip -u /path/to/vm/directory/moodle_app.zip -d /path/to/vm/directory/

                            # Implement custom logic to replace changed files
                            # This is a placeholder for your custom logic
                            # You can compare and replace only changed files here
                        '''
                    }
                }
            }
        }
    }
}
