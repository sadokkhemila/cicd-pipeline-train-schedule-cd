pipeline {
   agent any
   stages {
     stage('build') {
        steps {
            echo 'building'
            sh './gradlew build'
            archiveArtifacts artifacts: 'dist/trainSchedule.zip'
        }
     }
   }
}
