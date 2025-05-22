pipeline {
    agent any

    tools {
        msbuild 'VS_pr_build'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/stasyan04/lab4IT', credentialsId: 'github_jenkins_key', branch: 'master'
            }
        }
        
        stage('Build') {
            steps {
                bat '\"${MSBUILD}\" test_repos.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                bat "x64\\Debug\\test_repos.exe --gtest_output=xml:test_report.xml"
            }
        }
    }

    post {
        success {
            echo 'Build and tests were successful!'
        }
        failure {
            echo 'Something went wrong!'
        }
    }
}