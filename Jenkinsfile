node {
    stage("Git Clone"){
        git credentialsId: 'git_hub_cred', url: 'https://github.com/mahouESPRIT/spring-jenkins-test.git'
    }  
    
     stage('Gradle Build') {
       sh './gradlew build'
    }
    
    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t jhooq-docker-demo .'
        sh 'docker image list'
        sh 'docker tag jhooq-docker-demo ayoubmahou/jhooq-docker-demo:jhooq-docker-demo'
    }


}





