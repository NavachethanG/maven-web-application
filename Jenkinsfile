node {
    
def mavenHome = tool name: "maven 3.9.6"

//checkout code
stage('CheckoutCode'){
git branch: 'development', url: 'https://github.com/NavachethanG/maven-web-application.git'
}

//Build Stage
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

//SonarQube Report
stage('SonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

//Upload Artifacts into Artifact Repo
stage('UploadArtifactintoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

//Deploy App into Tomcat server
stage('DeployAppintoTomcat'){
sshagent(['cd4702b8-c316-433d-863f-7a00342fd5fc']){
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.235.254.132:/opt/apache-tomcat-9.0.85/webapps"
}
}

}
