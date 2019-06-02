node
{
    def mavenHome = tool name: 'maven-3.6.1', type: 'maven'
    
    stage ('GitHub_Pull')
    {
        git credentialsId: 'Git-Jenkins', url: 'https://github.com/karrikavya/maven-web-application.git'
    }
    
    stage ('Build_Maven')
    {
        sh "${mavenHome}/bin/mvn clean package"
    }
    
    stage ('Nexus_Push')
    {
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
    stage ('SonarQube_Push')
    {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
    stage ('Deploy_Tomcat')
    {
        sh "scp ${WORKSPACE}/target/*.war ec2-user@13.232.55.202:/opt/apache-tomcat-9.0.20/webapps"    
    }
    
 }
