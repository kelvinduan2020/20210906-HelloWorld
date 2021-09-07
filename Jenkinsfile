node{
    stage('Git Checkout'){
        git 'https://github.com/kelvinduan2020/20210906-HelloWorld.git'
    }
    stage('Maven Build'){
        sh 'mvn clean install package'
    }
    withCredentials([string(credentialsId: 'docker-hub-password', variable: 'docker-hub-pwd')]) {
        stage('Build Docker Image And Push to DockerHub'){
            ansiblePlaybook credentialsId: 'ansible-to-webapp', 
                            extras: "docker_hub_pwd=${docker-hub-pwd}", 
                            installation: 'ansible', 
                            inventory: 'host.inv', 
                            playbook: 'CreateDockerImageByAnsible.yml'
        }
    }
}
