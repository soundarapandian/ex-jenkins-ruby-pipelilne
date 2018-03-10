pipeline {
  agent { label 'ruby' }

  triggers {
    pollSCM('* * * * *')
  }

  stages {
      stage('Checkout') {
          steps {

              checkout([$class: 'GitSCM',
                  branches: [[name: "*/master"]],
                  doGenerateSubmoduleConfigurations: false,
                  userRemoteConfigs: [[ url: 'https://github.com/soundarapandian/ex-ruby-jenkins-build.git', permissions: 'READABLE']]])
          }
      }
      stage('Install') {
          steps {
              sh '''#!/bin/bash -l
                    rvm use 2.2.2
                    gem install bundler
                    bundle install
              '''
          }
      }
      stage('Test') {
        steps {
          sh '/bin/bash -l -c "rvm use 2.2.2 && bundle exec rspec"'
        }
      }
  }
}
