pipeline
{
	agent any
	
	stages
	{
		stage('Clone')
		{
			checkout scm
		}
		stage('Clean')
		{
			sh '/root/apache-maven-3.6.3/bin/mvn clean'
		}
		stage('Build')
		{
			sh '/root/apache-maven-3.6.3/bin/mvn install'
		}
		stage('Deployment')
		{
			echo "Project has been built"
		}
	}
}
