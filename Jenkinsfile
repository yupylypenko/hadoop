def checkFolderForDiffs(path) {
    try {
        // git diff will return 1 for changes (failure) which is caught in catch, or
        // 0 meaning no changes
        sh "git diff --quiet --exit-code HEAD~1..HEAD ${path}"
        return false
        } catch (err) {
        return true
        }
      }

pipeline {
    agent any
    stages {
        stage('Check playbook depends on comment') {
            steps {
              echo 'Start the check of playbooks '
              script {

                if ( checkFolderForDiffs("ansible/roles/local_docker")){
                  echo 'I only execute on the master branch'
                } else {
                  echo 'I execute elsewhere'
                }

              }
            }
        }
        stage('Deploy playbooks depends on comment') {
            steps {
              echo 'Start deploying playbook'
              script {

                if ( checkFolderForDiffs("ansible/roles/local_docker")){
                  echo 'I only execute on the master branch'
                } else {
                  echo 'I execute elsewhere'
                }

              }
            }
        }
    }
}
