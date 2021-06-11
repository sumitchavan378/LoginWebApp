pipeline
{
	agent any
	triggers
	{
		pollSCM('* * * * *')
	}
	parameters
	{
		choice(name: 'Server', choices:['Loginwebapp1', 'Loginwebapp2'])
		string(name: 'password', defaultValue: 'devops')
	}
	stages
	{
		stage('Clone')
		{
			steps
			{
				echo "Cloned"
			}
		}
		stage('Build')
		{
			steps
			{
				sh 'mvn install'
			}
		}
		stage('Deployment')
		{
			steps
			{
				script
				{	
					if ( Server == "Loginwebapp1" )
					{
						sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/'
					}
				
					else if ( Server == "Loginwebapp2"  )
					{
						sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/'
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
