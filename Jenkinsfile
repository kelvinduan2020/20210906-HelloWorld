node{
    stage('Git Checkout'){
        git 'https://github.com/kelvinduan2020/20210906-HelloWorld.git'
    }
    stage('Maven Build'){
        sh 'mvn clean install package'
    }
    stage('Build Docker Image'){
        //sh 'docker build -t kelvinduan/webapp:latest .'
        ansiblePlaybook credentialsId: 'ansible-to-webapp', extras: '--limit localhost', installation: 'ansible', inventory: 'host.inv', playbook: 'CreateDockerImageByAnsible.yml'
    }
}
