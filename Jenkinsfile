pipeline {
    agent any
    parameters {
        choice(
            name: 'environment', 
            choices: ['staging', 'perf', 'smoke', 'prod'], 
            description: 'Select environment'
        )
        choice(
            name: 'deployType', 
            choices: ['regular update', 'restart from timestamp'], 
            description: 'Deploy type'
        )
    }
    stages {
        stage('Initial Selection') {
            steps {
                script {
                    // Display initial parameter selection
                    echo "Selected environment: ${params.environment}"
                    echo "Selected deploy type: ${params.deployType}"
                    
                    // Fetch additional parameters based on initial selection
                    def additionalParams = fetchAdditionalParams(params.environment, params.deployType)
                    
                    // Rebuild parameters for the second screen
                    currentBuild.description = "Continue to next screen with additional parameters"
                    input message: 'Proceed with additional inputs?', parameters: additionalParams
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Add your deployment logic here
                    echo "Proceeding with deployment..."
                    echo "Environment: ${params.environment}"
                    echo "Deploy Type: ${params.deployType}"
                    
                    // Retrieve and display additional parameters
                    echo "Additional Parameters: ${params}"
                    
                    // Implement your deployment logic based on selected parameters
                    deployApplication(params)
                }
            }
        }
    }
}

def fetchAdditionalParams(env, deployType) {
    def additionalParams = []
    
    if (env == 'staging') {
        additionalParams.add(string(name: 'stagingParam', defaultValue: '', description: 'Additional parameter for staging'))
    } else if (env == 'perf') {
        additionalParams.add(string(name: 'perfParam', defaultValue: '', description: 'Additional parameter for performance'))
    } else if (env == 'smoke') {
        additionalParams.add(string(name: 'smokeParam', defaultValue: '', description: 'Additional parameter for smoke tests'))
    } else if (env == 'prod') {
        additionalParams.add(string(name: 'prodParam', defaultValue: '', description: 'Additional parameter for production'))
    }

    // Add common additional parameters
    additionalParams.add(string(name: 'commonParam', defaultValue: '', description: 'Common additional parameter for all environments'))
    
    return additionalParams
}

def deployApplication(params) {
    // Your deployment logic based on parameters
    if (params.environment == 'staging') {
        echo "Deploying to staging environment with parameter: ${params.stagingParam}"
    } else if (params.environment == 'perf') {
        echo "Deploying to performance environment with parameter: ${params.perfParam}"
    } else if (params.environment == 'smoke') {
        echo "Deploying to smoke environment with parameter: ${params.smokeParam}"
    } else if (params.environment == 'prod') {
        echo "Deploying to production environment with parameter: ${params.prodParam}"
    }
    
    echo "Using common parameter: ${params.commonParam}"
}
