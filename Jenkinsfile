pipeline {
    agent any

    stages {
        stage('verify branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
         stage('Create file') {
            steps {
                writeFile file: 'testfile.txt', text: 'Hare Krishna'
            }
        }
    }
}
