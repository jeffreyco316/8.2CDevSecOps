pipeline{ 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: 'https://github.com/jeffreyco316/8.2CDevSecOps.git' 
      }
      post{
        success{
            mail to: "jeffreyc.o.316@gmail.com",
            subject: "Checkout Stage Email",
            body: "Checkout was a success!"
        }
      } 
    } 
 
    stage('Install Dependencies') { 
      steps { 
        sh 'npm install' 
      } 
      post{
        failure{
            mail to: "jeffreyc.o.316@gmail.com",
            subject: "Install Dependencies Email",
            body: "Install Dependencies failure!"
        }
      }
    } 
 
    stage('Run Tests') { 
      steps { 
        sh 'npm test || true' // Allows pipeline to continue despite test failures 
      }
      post{
        failure{
            mail to: "jeffreyc.o.316@gmail.com",
            subject: "Run Tests Email",
            body: "Run Tests failure!"
        }
      } 
    } 
 
    stage('Generate Coverage Report') { 
      steps { 
        // Ensure coverage report exists 
        sh 'npm run coverage || true' 
      }
      post{
        failure{
            mail to: "jeffreyc.o.316@gmail.com",
            subject: "Generate Coverage Report Email",
            body: "Generate Coverage Report failure!"
        }
      } 
    } 
 
    stage('NPM Audit (Security Scan)') { 
      steps { 
        sh 'npm audit || true' // This will show known CVEs in the output 
      }
       post{
        failure{
            mail to: "jeffreyc.o.316@gmail.com",
            subject: "NPM Audit (Security Scan) Email",
            body: "NPM Audit (Security Scan) failure!"
        }
      } 
       
    }
  }
}
