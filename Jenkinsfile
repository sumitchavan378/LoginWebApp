pipeline
{
	agent any
	triggers
	{
		pollSCM('* * * * *')
	}
	parameters
	{
		choice(name: 'Server', choices: ['Loginwebapp1', 'Loginwebapp2'])
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
					echo "Project has been built $Server"
					if ( Server == "Loginwebapp1")
					{
						echo "You have selected Loginwebapp1"
					}
					else if ( Server == "Loginwebapp2" )
					{
						echo "You have selected Loginwebapp2"
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
