node{

    docker.image('jekyll/builder').inside {
    checkout scm 
    stage("Build") {
      sh "ls"  
      sh "jekyll build"
    }

}
}
