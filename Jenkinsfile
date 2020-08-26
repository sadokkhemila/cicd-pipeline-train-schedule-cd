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
      stage('deploy to staging') {
         when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'webserver_login', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'dist/trainSchedule.zip',
                                        removePrefix: 'dist/',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'sudo /usr/bin/systemctl stop train-schedule-cd && rm -rf /opt/train-schedule-cd/* && unzip /tmp/trainSchedule-cd.zip -d /opt/train-schedule-cd && sudo /usr/bin/systemctl start train-schedule-cd'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
      }
   }
}
