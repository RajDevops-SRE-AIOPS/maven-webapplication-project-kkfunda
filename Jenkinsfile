node
{
    //   /var/lib/jenkins/tools/hudson.tasks.Maven_MavenInstallation/Maven-3.9.16
   def mavenHome=tool name: "Maven-3.9.16"
   stage('git checkout')
   {
     git branch: 'master', url: 'https://github.com/RajDevops-SRE-AIOPS/maven-webapplication-project-kkfunda.git'
   }
   stage('compile')
   {
    sh "${mavenHome}/bin/mvn compile"
   }

   stage('Build')
   {
    sh "${mavenHome}/bin/mvn clean package"
   }
   stage('SQ Report')
   {
    sh "${mavenHome}/bin/mvn sonar:sonar"
   }

   stage('Deploy Into Nexus')
   {
    sh "${mavenHome}/bin/mvn clean deploy"
   }

    stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u kk:password \
--upload-file /var/lib/jenkins/workspace/Scripted-Way-Pipeline/target/maven-web-application.war \
"http://13.232.165.81:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }

	
}  //node ending
