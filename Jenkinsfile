pipeline {
    agent { label 'DOCKER'}
    trigeers { pollScm('* * * * 1-5') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'git@github.com:Nagaraju11111/StudentCoursesRestAPI.git'
                    branch: 'master'
            }
        }
        stage ('image build') {
            steps {
                sh """
                    docker image build -t src:1.0 .
                    docker image tag src:1.0 9052171017/src:1.0
                    docker image push 9052171017/src:1.0
                """
            }
        }
           stage ('container') {
            steps {
                sh """
                    docker image ls
                    docker image pull 9052171017/src:1.0
                    docker container run -d -P --name sc1 9052171017/src:1.0
                """
            }
        }
    }
}