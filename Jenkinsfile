
pipeline {
    agent any 
    tools {
        maven "maven-3.9.8" // Ensure this matches the name in your Jenkins Global Tool Configuration
    }

    stages {
        stage 1 :('Checkout Stage') { 
            steps {
                // Cloning the code from the GitHub repository
                git branch: 'fea', url: 'https://github.com/lokeshreddys108/maven-webapplication-project-kkfunda.git'
            }
        }

        // Stage 2: Maven Build, Sonar scan, and Nexus deploy (Run in parallel)
        stage('Maven, Sonar, and Nexus') {
            steps {
                parallel (
                    "Build": {
                        sh "mvn clean package"  // Run Maven build
                    },
                    "Sonar": {
                        sh "mvn sonar:sonar"  // Run Sonar scan
                    },
                    "Nexus": {
                        sh "mvn deploy"  // Deploy to Nexus repository
                    }
                )
            }
        }
    }
}
