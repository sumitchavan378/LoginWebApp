pipeline
{
    agent any
    triggers
    {
        pollSCM('* * 30 * *')
    }
    parameters
    {
        choice(name: 'Server', choices: ['Loginwebapp1','Loginwebapp2', 'all'])
        string(name: 'password', defaultValue: 'devops')
    }
    stages
    {
        stage('Cloning')
        {
            steps
            {
                checkout scm
            }
        }
        stage('Maven Tasks')
        {
            parallel
            {
                stage('Clean')
                {
                    steps
                    {
                        sh '/root/apache-maven-3.6.3/bin/mvn clean'
                    }
                }
                stage('Build')
                {
                    steps
                    {
                        sh '/root/apache-maven-3.6.3/bin/mvn install'
                    }
                }
            }
        }
        stage('Deployment')
        {
            steps
            {
		
            	sh(returnStdout: true, script: '''#!/bin/bash
            	if [ $Server == "Loginwebapp1" ];
		then
                	if [ $? -eq 0 ];
			then
	                        sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/
				echo "WAR has been deployed successfully"
                        else
                                echo "Something went wrong"
                        fi
                  
		elif [ $Server == "Loginwebapp2" ];
		then
                    	sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/
                    
                elif [ $Server == "all" ];
		then
                    	sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/
                        sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/
                else
                
                        echo "Wrong Choice"
                fi

        	'''.stripIndent())   
		    
                
            }
        }
    }
}
