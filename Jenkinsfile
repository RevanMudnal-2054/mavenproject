pipeline {
  agent any  // Run on any available Jenkins agent

  stages {
    // Step 1: Get the code
    stage('Clone') {
      steps {
        git 'https://github.com/RevanMudnal-2054/mavenproject.git'
      }
    }

    // Step 2: Build the code into a .war file
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

    // Step 3: Send the .war file to the Green server
    stage('Deploy to Green') {
      steps {
        // Use saved SSH credentials (called 'green-server-ssh')
        sshagent(['green-server-ssh']) {
          // Copy .war file to Green server using scp
          sh 'scp target/*.war ubuntu@<54.242.0.137>:/opt/tomcat/webapps/'
        }
      }
    }
  }
}
