pipeline
{
	agent any
	stages
	{
		stage('Clone')
		{
			steps
			{
				checkout SCM
			}
		}
		stage('Build')
		{
			steps
			{
				sh '/root/apache-maven-3.6.3/bin mvn install'
			}
		}
		stage('Deployment')
		{
			steps
			{
				script
				{
					echo "Project has been built"
				}
			}
		}
	}
}
