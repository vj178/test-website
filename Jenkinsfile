node{
    checkout scm 
    docker.image('jekyll/jekyll').inside {

    stage("Build") {
      sh "jekyll build"
    }

}
}
