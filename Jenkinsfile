pipeline {
    agent any
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/SRIVATSA2002/Petclinic.git'
            }
        }
        
        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Petclinic \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=Petclinic '''
    
                }
            }
        }
        
        stage("OWASP Dependency Check"){
            steps{
                dependencyCheck additionalArguments: '--scan ./ --format HTML ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }
    }
}
