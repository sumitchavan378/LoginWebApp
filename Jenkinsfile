pipeline
{
	agent any
	parameters
	{
		choice(name: 'Server', choices: ['Loginwebapp1','Loginwebapp2'])
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
					if ( Server == 'LoginWebApp1' ) 
					{			
				   		echo "WAR has been deployed on Loginwebapp1"
					}
					else if ( Server == 'LoginWebApp2' )
					{
						echo "WAR has been deployed on Loginwebapp2"
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
