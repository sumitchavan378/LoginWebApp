pipeline
{
	agent any
	triggers
	{
		pollSCM('* * 30 * *')
	}
	parameters
	{
		choice(name: Server, choices:['Loginwebapp1', 'Loginwebapp2'])
		string(name: password, defaultValue: devops)
	}
	stages
	{
		stage('clone')
		{
			steps
			{
				echo "Cloned"
			}
		}
	}
}
