pipeline
{
	agent any
	parameters
	{
		choice(name: 'Server', choices: ['LoginWebApp1','LoginWebApp2'])
		string(name: 'password', trim: true)
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
					if (Server == 'LoginWebApp1') 
					{
						sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/'			
				   		echo "WAR has been deployed on Loginwebapp1"
					}
					else if (Server == 'LoginWebApp2')
					{
						sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/'
						echo "WAR has been deployed on Loginwebapp2"
					}
					

				}
			}
		}
	}
}
