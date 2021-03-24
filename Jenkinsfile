pipeline {
    agent any

    stages {
        stage('verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
         stage('Docker build') {
            steps {
                sh(script: 'docker images -a')
                sh(script: """
                cd azure-vote/
                docker images -a
                docker build -t jenkins-pipeline .
                cd ..
                """)
            }
        }
        stage('start test') {
            steps {
                sh(script: """
                docker-compose up -d
                ./scripts/test_container.sh
                """)
            }
            post{
                success{
                    echo "success app start"
                }
                failure{
                     echo "failure app start"
                }
            }
        }
        stage('run test') {
            steps {
                sh(script: """
                pytest ./tests/test_sample.py
                """)
            }
        }
        stage('stop test') {
            steps {
                sh(script: """
                docker-compose down
                """)
            }
        }
    }
}
