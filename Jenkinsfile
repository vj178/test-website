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
        sh 'echo TEST'  
      sh 'SSHPASS=$PASSWORD sshpass -e ssh -l $USERNAME ${env.HOST} rm -rf /home/vijay/_site/*'
      sh 'SSHPASS=$PASSWORD sshpass -e scp -r _site/* $USERNAME@${env.HOST}:/home/vijay/_site/'
    }
  }
}
