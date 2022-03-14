node {
    def mvnhome = tool name: 'Maven-home', type: 'maven'  
    stage('scm checkout') { 
        git branch: 'main', credentialsId: 'Git-credentials', url: 'https://github.com/mbinui/tomcat-demo.git'
        } 
    stage('Maven-clean') {      
        sh "${mvnhome}/bin/mvn clean"
	} 
    stage('Maven-compile') {      
        sh "${mvnhome}/bin/mvn compile"
    }
    stage('Maven-package') {      
        sh "${mvnhome}/bin/mvn package"
    }
    stage('Tomcat-deployment') { 
        sshagent(['ec2-user']) {
            sh 'scp -o StrictHostKeyChecking=no target/tomcat-demo.war ec2-user@172.31.46.181:/opt/mytomcat/webapps/'
		}
    }
}
