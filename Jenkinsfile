
pipeline {
    agent any 
    tools {
        maven "maven-3.9.8" // Ensure this matches the name in your Jenkins Global Tool Configuration
    }

    stages {
        stage('Checkout Stage') { 
            steps {
                // Cloning the code from the GitHub repository
                git branch: 'fea', url: 'https://github.com/lokeshreddys108/maven-webapplication-project-kkfunda.git'
            }
        }

        stage('Build') { 
            steps {
                // Building the project with Maven
                sh 'mvn clean package'
            }
        }

        stage('SQReport') {
            steps {
                // Running the SonarQube analysis
                sh 'mvn sonar:sonar'
            }
        }

        stage('DeployToNexus') {
            steps {
                // Deploying the project to Nexus
                sh 'mvn deploy'
            }
        }

        stage('DeployAppToTomcat') {
            steps {
                // Deploying the WAR file to Tomcat
                echo "Deploying WAR file to Tomcat..."

                sh """
                      curl -u kk:password \
        --upload-file /var/lib/jenkins/workspace/Declarative-pipeline/target/maven-web-application.war \
        "http://54.160.224.158:8080/manager/text/deploy?path=/maven-web-application&update=true"
                """
            }
        }
    }
}
