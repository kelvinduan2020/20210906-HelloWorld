node{
    stage('Git Checkout'){
        git 'https://github.com/kelvinduan2020/20210906-MavenProject.git'
    }
    
    stage('Maven Build'){
        sh 'mvn clean install package'
    }
    
    stage('Create Docker Image'){
        ansiblePlaybook credentialsId: 'ansible-to-webapp',
                        installation: 'ansible', 
                        inventory: 'ansible/host.inv', 
                        playbook: 'ansible/CreateDockerImage.yml'
    }
    
    withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerHubPWD')]) {
        stage('Push to DockerHub'){
            ansiblePlaybook credentialsId: 'ansible-to-webapp', 
                            installation: 'ansible', 
                            inventory: 'ansible/host.inv',
                            playbook: 'ansible/PushToDockerHub.yml',  
                            extras: "-e docker_hub_pwd=${dockerHubPWD}"
        }
    }
    
    stage('Run On Container'){
        ansiblePlaybook credentialsId: 'ansible-to-webapp', 
                        installation: 'ansible', 
                        inventory: 'ansible/host.inv', 
                        playbook: 'ansible/DeployOnContainer.yml'
    }
    }
}
