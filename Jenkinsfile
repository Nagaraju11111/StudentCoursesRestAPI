pipeline {
    agent any
    triggers { pollSCM('* * * * 1-5') }
    stages {
        stage ('vcs') {
            steps {
                git url: 'https://github.com/Nagaraju11111/StudentCoursesRestAPI.git',
                    branch: 'master'
            }
        }
        stage ('image build') {
            steps {
                sh """
                    docker image build -t srcdev:1.0 .
                    docker image tag srcdev:1.0 9052171017/srcdev:1.0
                    docker image push 9052171017/srcdev:1.0
                """
            }
        }
           stage ('k8s deploy') {
            steps {
                sh """
                    kubectl apply -f k8s/sqlpvc.yaml
                    kubectl apply -f k8s/sqldb.yaml
                    kubectl applyy -f k8s/srcapp.yaml
                    
                """
            }
        }
    }
}
