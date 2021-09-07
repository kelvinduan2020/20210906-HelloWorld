node{
    stage('Maven Build') {
        withMaven(maven: 'maven') {
            sh 'mvn clean install package'
        }
    } 
}
