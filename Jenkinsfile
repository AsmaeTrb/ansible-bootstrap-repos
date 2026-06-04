pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "✅ Code récupéré depuis Git"
            }
        }

        stage('Create Bootstrap Repositories') {
            steps {
                sshagent(credentials: ['ansible-ssh']) {
                    sh '''
                        ansible-playbook playbooks/create_bootstrap_repos.yml
                    '''
                }
            }
        }
    }

    post {
        success {
            echo '✅ Vérification des synchronisations et création des bootstrap repositories terminées avec succès !'
        }
        failure {
            echo '❌ Erreur pendant le pipeline bootstrap repositories !'
        }
    }
}
