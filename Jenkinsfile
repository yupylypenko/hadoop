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

                if ( checkFolderForDiffs("ansible/roles/local_docker")||checkFolderForDiffs("ansible/playbooks/local_docker_cluster.yml")){
                  ansiblePlaybook(
                    //credentialsId: '4908ee95-1fbb-45d0-b1b6-0f45cd7f5160',
                    inventory: 'inventory/docker/hosts-inventory',
                    playbook: 'playbooks/local_docker_cluster.yml',
                    extras: '--check',
                    colorized: true,
                    //tags: 'ditto_dags'
                 )
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

                if ( checkFolderForDiffs("ansible/roles/local_docker")||checkFolderForDiffs("ansible/playbooks/local_docker_cluster.yml")){
                  ansiblePlaybook(
                    //credentialsId: '4908ee95-1fbb-45d0-b1b6-0f45cd7f5160',
                    inventory: 'inventory/docker/hosts-inventory',
                    playbook: 'playbooks/local/local_docker_cluster.yml',
                    colorized: true,
                    //tags: 'ditto_dags'
                 )
                } else {
                  echo 'I execute elsewhere'
                }

              }
            }
        }
    }
}
