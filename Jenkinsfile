pipeline {
  agent {
    kubernetes {
      // Define the pod template with container template
      containerTemplate {
            name 'gradle'
            image 'gradle'
            command 'sleep'
            args '30d'
        }
    }
  }
  
  stages {
    stage('Checkout code and prepare environment') {
      steps {
        git url: 'https://github.com/bingbingkuai/chp5.git', branch: 'master'
        sh ''' 
          cd Chapter08/sample1
          chmod +x gradlew
        ''' 
      }
    }

    stage('Run pipeline against a gradle project - main branch') {
      when {
        branch 'main'
      }
      steps {
         echo 'On main branch'

         sh ''' 
         pwd
         cd Chapter08/sample1
         ./gradlew test
         ./gradlew jacocoTestCoverageVerification
         '''
      }
    }


    stage('Run pipeline against a gradle project - br1') {
      when {
         branch 'br1' 
      }
      steps {
         echo 'Unit test on br1'

         sh ''' 
			pwd
          cd Chapter08/sample1; 
          ./gradlew checkstyleMain
         ''' 
      }
    }

    stage('Run pipeline against a gradle project - br2') {
      when {
         branch 'br2' 
      }
      steps {
         echo 'This is on br2'

         sh ''' 
			pwd
          cd Chapter08/sample1; 
          ls
         ''' 
      }
    }

  }
}
