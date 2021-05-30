pipeline
{
	agent any
	parameters
	{
		choice(name: 'Server', choices: ['Loginwebapp1','Loginwebapp2'])
		string(name: 'password')
	}
	stages
	{
		stage('Clone')
		{
			steps
			{
				checkout scm
			}
		}
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
		stage('Deployment')
		{
			steps
			{
				script
				{
					echo "You have selected $Server to deploy WAR"
					if ( $Server == LoginWebApp1 ) 
					{
					sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/
				
				   	echo "WAR has been deployed on $Server"
					}
					else if ( $Server == LoginWebApp2 )
					{
					sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/
					echo "WAR has been deployed on $Server"
					}
					else if ( $all == true )   
					{
					sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/
	    			        sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/
				  	echo "Deployed WAR to ALL Servers"
					}
					else
					{
					echo "Wrong Choice"
					}
					

				}
			}
		}
	}
}
