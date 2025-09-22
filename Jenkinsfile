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
        stage ("Deliver for development") {
            when { 
                branch 'development'
            } 
            steps {
                container('nodejs') {
                    sh './jenkins/scripts/deliver-for-development.sh'
                    input message: 'Finished using the web site? (Click "Proceed" to continue)'
                    sh './jenkins/scripts/kill.sh'
                }
                
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'  
            }
            steps {
                container('nodejs') {
                    sh './jenkins/scripts/deploy-for-production.sh'
                    input message: 'Finished using the web site? (Click "Proceed" to continue)'
                    sh './jenkins/scripts/kill.sh'
                }
            }
        }
     }
}   