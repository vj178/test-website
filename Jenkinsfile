node{

    docker.image('ruby:latest').inside {
    checkout scm 
    stage("Build") {
      sh "bundle"
      sh "jekyll build"
      archive '_site/**'

      stash includes: '_site/**', name: 'built-site' 
    }

}
}

if (currentBuild.result == 'UNSTABLE') {
  echo 'Skipping deployment due to unstable build'
} else {

  stage 'Deploy'
  node() {
    deleteDir()
    unstash 'built-site'

    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'website', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME']]) {
      sh 'SSHPASS=$PASSWORD sshpass -e ssh -o StrictHostKeyChecking=no -l $USERNAME $HOST rm -rf /home/vijay/_site/*'
      sh 'SSHPASS=$PASSWORD sshpass -e scp -o StrictHostKeyChecking=no -r _site/* $USERNAME@$HOST:/home/vijay/_site/'
    }
  }
}
