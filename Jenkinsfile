node{
    stage('Git Checkout'){
        git 'https://github.com/kelvinduan2020/20210906-HelloWorld.git'
    }
    stage('Maven Build'){
        sh 'mvn clean install package'
    } 
}
