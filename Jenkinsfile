pipeline
{
	agent
	{
                label 'Loginwebapp2'
        }
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
				checkout scm
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
