node{

    docker.image('jekyll/jekyll').inside {
    checkout scm 
    stage("Build") {
      sh "jekyll build"
    }

}
}
