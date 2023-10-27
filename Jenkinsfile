node{
    
    def mavenHome = tool name: "maven3.9.4"
    
    stage('CheckOutCode'){
git branch: 'development', credentialsId: '8348f8f0-25de-414b-be0c-6b5259e01762', url: 'https://github.com/sreeharikabadrisetty/maven-web-application.git'
     
    }
    
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage('ExecuteSonarQubeReport'){
        sh "${mavenHome}/bin/mvn clean sonar:sonar"
    }
    stage('UploadArtifactsIntoNexus'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeployAppIntoTomcatServer'){
        sshagent(['6df8e93a-bdcd-469b-a00c-86aac781e175']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.14.85.250:/opt/apache-tomcat-9.0.80/webapps/"
    // some block
}
    }
}//node closing
