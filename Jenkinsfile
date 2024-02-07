pipeline
{
    agent any
    
    tools
    {
    maven 'maven-3.9.6'
    }


    stages
    {
        stage('welcome')
        {
            steps
            {
              echo "hello"  
            }
        }
    
    
    
    
        stage('checkout')
        {
            steps
            {
            git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/NooraynAbdulraufAttar/mywebapp.git'
            }
        }
    
    
        stage('code build')
        {
            steps
            {
            sh 'mvn clean package'
            }
        }
    
        stage('code analysis')
        {
            steps
            {
             jacoco maximumBranchCoverage: '80', maximumClassCoverage: '80', maximumComplexityCoverage: '80', maximumInstructionCoverage: '80', maximumLineCoverage: '80', maximumMethodCoverage: '80', minimumBranchCoverage: '80', minimumClassCoverage: '80', minimumComplexityCoverage: '80', minimumInstructionCoverage: '80', minimumLineCoverage: '80', minimumMethodCoverage: '80'
            }
        }
        
        
        
        stage('static analysis')
        {
            steps
            {
             recordIssues(tools: [checkStyle(), pmdParser()])
            }
        }
        
         stage('docker build')
        {
          steps
          {
           withCredentials([usernamePassword(credentialsId: 'tuktuka-docker', passwordVariable: 'pwd', usernameVariable: 'uname')])
               {
            
              sh 'docker login -u ${uname} -p dckr_pat_7rSmxdZl2f520cBVsYAUQXovqos'
              sh 'docker build -t tuktuka/jenkinsdemog .'
              sh 'docker push tuktuka/jenkinsdemog'
                
                }
                 
          
            }
        }
            
    }    
    
        
        
    
}
    
