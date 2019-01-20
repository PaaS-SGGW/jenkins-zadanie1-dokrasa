node {
    agent any
    
    stage('Raz'){
        sh 'git config --global user.email "test@test.com"'
        sh 'git config --global user.name "ci-bot"'
        sh 'git config --global credential.helper cache'
        sh "git config --global credential.helper 'cache --timeout=3600'"
    }
    
    stage('Dwa'){
        git credentialsId: 'dokrasa', url: 'https://github.com/PaaS-SGGW/zadanie-0-konto-dokrasa'
        git credentialsId: 'dokrasa', url: 'https://github.com/dokrasa/sggw-mgr-2-paas'
    }

    stage('Trzy'){
        sh 'git clone --bare https://github.com/PaaS-SGGW/zadanie-0-konto-dokrasa tfs'
        dir("tfs") {
            sh 'git remote add --mirror=fetch heroku https://github.com/dokrasa/sggw-mgr-2-paas'
            sh 'git fetch origin --tags'

            sh 'git fetch heroku --tags'

            sh 'git push heroku --all'
            sh 'git push heroku --tags'
        }
    }
}
