pipeline { 
    agent {
       label "kubeagent"
    } 
    environment { 
        CI = "true"
    }
    stages {
        stage ("Build") { 
            steps {
                container('nodejs') {
                    sh "npm install"
                }
            }
        }
        stage ("Test") { 
            steps {
                container('nodejs') {
                    sh "./jenkins/scripts/test.sh"
                }
            }
        }   
    }
}   