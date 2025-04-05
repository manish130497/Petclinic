pipeline { agent any

stages {
    stage('Clone') {
        steps {
            git branch: 'main', url: 'https://github.com/manish130497/Petclinic.git'
        }
    }
    stage('Build the project') {
        steps {
            sh 'mvn package'
        }
    }
    
    stage('Test') {
        steps {
            sh 'mvn test'
        }
    }
    stage('publish Test Results') {
        steps {
            junit 'target/surefire-reports/*.xml'
        }
    }
    
    stage('Publish the Artifacts') {
        steps {
    archiveArtifacts artifacts: '**target/*.war', followSymlinks: false      }
    }

        stage('Deploy to Tomcat server') {
        steps {
            deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://localhost:8080/')], contextPath: 'Devops', war: 'target/*.war'
        }
     }    
   }
 }