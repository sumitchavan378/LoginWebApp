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
				echo "Project has been built $Server"
			}
		}
	}
}
