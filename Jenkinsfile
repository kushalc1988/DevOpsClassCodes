
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
    agent none
      stages{
           stage('Checkout'){
		   agent {label 'Dev'}
               steps{
		 echo 'cloning..'
                 git 'https://github.com/Sonal0409/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
              agent {label 'Dev'}
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
              agent {label 'Dev'}
              steps{
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		   agent {label 'Dev'}
              steps{
	         
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
           stage('MetricCheck'){
               agent {label 'Dev'}
              steps{
                  sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
              }
               post {
               success {
	           cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false                  
               }
           }		
          }
          stage('Package'){
              agent {label 'Dev'}
              steps{
                  sh 'mvn package'
              }
          }
	     
          
      }
}
