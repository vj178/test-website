node{

    docker.image('jekyll/builder').inside {
    checkout scm 
    stage("Build") {
      sh "jekyll build"
      sh "ls _site"  
    }

}
}
