pipeline{

        agent {
                node {
                        label "slave-1"
                        }
                }
    

        stages {
                stage ("delete"){
			steps {
			sh "cd /mnt/jenkins_slave1/workspace/war_build_deploy_in_slave"
			sh "rm -rf *"	
			} 
			}
			
		 stage ("maven_install"){
		     steps{
		         sh "wget https://dlcdn.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.zip"
		         sh "unzip apache-maven-3.9.5-bin.zip"
		         sh "rm -rf apache-maven-3.9.5-bin.zip"
		     }
		 }	

		stage ("github repo") {
                        steps {
                            sh 'sudo yum install git -y'
                           	git url: 'https://github.com/NamanBahre/project.git'

                   dir("/mnt/jenkins_slave1/workspace/war_build_deploy_in_slave"){
                    sh "/mnt/jenkins_slave1/workspace/war_build_deploy_in_slave/apache-maven-3.9.5/bin/mvn clean install"
                   }
                                }
                        } 

		stage ("copy_paste"){
			steps {
				sh "cp -r /mnt/jenkins_slave1/workspace/war_build_deploy_in_slave/target/*.war /mnt/servers/apache-tomcat-9.0.83/webapps/ "
			//	sh "chmod -R 777 /mnt/servers/apache-tomcat-9.0.83/webapps/"

				}
			}
                }

}
