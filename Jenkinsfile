pipeline {
  agent {
    docker {
      image 'circleci/ruby:2.6.0'
    }

  }
  stages {
    stage('build') {
      steps {
        sh 'gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/'
        sh 'sudo gem install bundler -f'
        sh 'bundle config mirror.https://rubygems.org https://gems.ruby-china.com'
        sh 'bundle install --jobs=4 --retry=3 --path vendor/bundle'
        sh 'bundle exec jekyll build'
      }
    }
    stage('deploy') {
      steps {
        sh 'wget -c http://collection.b0.upaiyun.com/softwares/upx/upx-linux-amd64-v0.2.3'
        sh 'mv upx-linux-amd64-v0.2.3 upx'
        sh 'chmod +x upx'
        sh './upx login yax-blog ${upx_USR} ${upx_PSW}'
        sh './upx sync _site/ / --delete'
      }
    }
  }
  environment {
    upx = credentials('upyun-account')
  }
}