pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Update Branches - create branch--requirements') {
            steps {
                script {
                    def selectedRepos = readFile('repo--requirements.txt').split('\n')
                    def branchesMap = [:]
                    
                    for (repo in selectedRepos) {
                        def gitBranches = sh(script: "git ls-remote --heads ${repo} | cut -f 2 | sed 's#refs/heads/##'", returnStdout: true).trim()
                        branchesMap[repo] = gitBranches.tokenize('\n')
                    }
                    writeFile file: 'branch--requirements.txt', text: branchesMap.collect { k, v -> "${k}:\n  ${v.join('\n  ')}" }.join('\n\n')
                }
            }
        }
    }
}
