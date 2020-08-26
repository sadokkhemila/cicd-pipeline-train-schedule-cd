pipeline {
   agent any
   stages {
     stage('build') {
        steps {
            echo 'building'
            ssh './gradlew build --no-daemon'
            archiveArtifacts artifacts: 'dist/trainSCedule.zip'
        }
     }
   }
}
