node{

    docker.image('ruby:latest').inside {
    checkout scm 
    stage("Build") {
      sh "bundle"
      sh "jekyll build --drafts"
      sh "ls _site"  
    }

}
}
