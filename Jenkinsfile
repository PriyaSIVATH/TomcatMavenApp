pipeline { 
    agent any
    tools {
        maven 'mvn-3.8.6'
    }
    stages {
        stage('Build') { 
            steps { 
                // sh '''
                bat '''
                    // echo "Added echo command"
                    mvn clean package
                '''
            }
        }
    }
}
