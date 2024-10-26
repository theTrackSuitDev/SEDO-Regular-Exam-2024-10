pipeline {
    agent any 
    stages {
        stage('Set currently changing branch') {
            steps {
                script {
                    def commit = checkout scm
                    env.BRANCH_NAME = commit.GIT_BRANCH.replace('origin/', '')
                }
            }
        }
            
        stage('Restore dependencies') { 
            when {
                branch "feature-ci-pipeline"
            }
    
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') { 
            when {
                branch "feature-ci-pipeline"
            }
            
            steps {
                sh 'dotnet build --no-restore' 
            }
        }
        stage('Test') {
            when {
                branch "feature-ci-pipeline"
            }
            
            steps {
                sh 'dotnet test --no-build --verbosity normal' 
            }
        }
    }
}
