node{
    stage('Git Checkout'){
        git 'https://github.com/kelvinduan2020/20210906-HelloWorld.git'
    }
    stage('Maven Build'){
        sh 'mvn clean install package'
    }
    withCredentials([string(credentialsId: 'docker-hub-password', variable: 'dockerHubPWD')]) {
        stage('Build Docker Image And Push to DockerHub'){
            ansiblePlaybook credentialsId: 'ansible-to-webapp', 
                            extras: "-e docker_hub_pwd=${dockerHubPWD}", 
                            installation: 'ansible', 
                            inventory: 'host.inv', 
                            playbook: 'CreateDockerImageByAnsible.yml'
        }
    }
}
