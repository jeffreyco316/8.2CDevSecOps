pipeline{ 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: 'https://github.com/jeffreyco316/8.2CDevSecOps.git' 
      }
    } 
 
    stage('Install Dependencies') { 
      steps { 
        bat 'npm install' 
      } 
    } 
 
    stage('Run Tests') { 
      steps { 
        bat 'npm test || exit /b 0' // Allows pipeline to continue despite test failures 
      }
      post{
        failure{
            emailext(
                attachLog: true,
                subject: "Run Tests Email",
                body: "Run Tests failure!",
                to: "jeffreyc.o.316@gmail.com"
            )

        }
      } 
    } 
 
    stage('Generate Coverage Report') { 
      steps { 
        // Ensure coverage report exists 
        bat 'npm run coverage || exit /b 0' 
      }
    } 
 
    stage('NPM Audit (Security Scan)') { 
      steps { 
        bat 'npm audit || exit /b 0' // This will show known CVEs in the output 
      }
       post{
        failure{
            emailext(
                attachLog: true, 
                subject: "NPM Audit (Security Scan) Email",
                body: "NPM Audit (Security Scan) failure!",
                to: "jeffreyc.o.316@gmail.com"
            )
        }
      } 
       
    }
  }
}
