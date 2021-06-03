pipeline
{
    agent any
    triggers
    {
        pollSCM('* * * * *')
    }
    parameters
    {
        choice(name: 'Server', choices: ['Loginwebapp1','Loginwebapp2', 'all'])
        string(name: 'password', defaultValue: 'devops')
    }
    stages
    {
        stage('Cloning')
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
                    if ( Server == "Loginwebapp1" )
                    {
                        sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/'
                    }
                    else if ( Server == "Loginwebapp2" )
                    {
                        sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/'
                    }
                    else if ( Server == "all" )
                    {
                        sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.2:/apache-tomcat-9.0.44/webapps/'
                        sh 'sshpass -p $password scp target/LoginWebApp.war root@172.17.0.3:/apache-tomcat-9.0.44/webapps/'
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
