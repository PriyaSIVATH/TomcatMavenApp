pipeline { 
    // agent any
    // docker { image 'ubuntu:latest' }
    agent {
        docker { image 'maven:amazoncorretto' }  
     }
    tools {
        maven 'mvn-3.9.0'
    }
    stages {
        stage('checkout') { 
            steps { 
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/PriyaSIVATH/TomcatMavenApp.git']])
            }
        }
        
        stage('Build') { 
            steps { 
                sh '''
                    mvn clean package
                '''
            }
        }
        
        /*stage('Archive Artifact') {
            steps {
                archiveArtifacts(artifacts: '**//*.jar', followSymlinks: false)
            }
         }*/

        stage('Artifact Upload to Nexus3') {
            steps {
              nexusArtifactUploader artifacts: [[artifactId: 'TomcatMavenApp', classifier: '', file: 'target/TomcatMavenApp-2.0-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus-repo-manager', groupId: 'MyTomcatMavenApp', nexusUrl: '192.168.0.155:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'devopsschool-hosted-snapshot', version: '2.0-SNAPSHOT'
            }
         }
        
    }
}