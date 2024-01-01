pipeline {
    agent any
  parameters {
        choice(choices: ['DEVELOPMENT', 'STAGING', 'PRODUCTION'], description: 'env type', name: 'ENVIRONMENT' )
        password(name: 'API_KEY', defaultValue: '123ABC', description: 'Enter the secret password')
        text(
            name: 'CHANGE_LOG',
            defaultValue: 'This is a Change Log',
            description: 'Enter a block of text:'
        )
        
    }
    stages {
        stage('Test'){
            steps{
                echo "This is the test stage"
            }
        }
        stage('Deploy'){
            when {
                expression {params.ENVIRONMENT == "PRODUCTION" }
            }
            steps{
                input message: 'Do you want to go ahead' , ok: 'open sesame'
                echo "Deploying to production environment"
            }
            
        }
        stage('Report'){
            steps{
                echo "Printing the report"
                echo "++++++++++++++++++++"
                sh "echo ${params.CHANGE_LOG}> ${params.ENVIRONMENT}.txt"
                archiveArtifacts artifacts: '*.txt', followSymlinks: false
                
            }
        }
    }
    
}
