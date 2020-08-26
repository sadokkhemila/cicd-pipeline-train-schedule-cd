pipeline {
   agent any
   stages {
     stage('build') {
        steps {
            echo 'building'
            ssh './gradlew build'
            archiveArtifacts artifacts: 'dist/trainSCedule.zip'
        }
     }
   }
}
