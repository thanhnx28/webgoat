pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/thanhnx28/webgoat.git'    //https://github.com/WebGoat/WebGoat.git
            }
        }
        stage('Test') {
            steps {
                sh '''
                    echo "Test by coverity scan"
                    coverity scan \
                    --project-dir $WORKSPACE \
                    --dir $WORKSPACE/idir \
                    -c /home/tiennv/cov-analysis-linux64-2025.3.0/bin \
                    --local-format html \
                    --local $WORKSPACE/results
                '''
            }
        }
    }
    post {
        success {
            echo '🎉 Build thành công!'
        }
        failure {
            echo '❌ Build thất bại.'
        }
        always {
            echo '🧹 Dọn dẹp thư mục idir...'
            sh 'rm -rf $WORKSPACE/idir'
        }
    }
}

