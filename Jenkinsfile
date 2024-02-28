pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        echo 'scm'
      }
    }

    stage('build') {
      parallel {
        stage('proxy') {
          steps {
            sh 'docker build -t proxy ./proxy'
          }
        }

        stage('db') {
          steps {
            sh 'echo \'db...\''
          }
        }

        stage('flask') {
          steps {
            sh 'docker build -t backend ./backend'
          }
        }

      }
    }

    stage('test images') {
      steps {
        sh 'docker images'
      }
    }

    stage('deploy') {
      steps {
        sh 'docker compose up -d'
      }
    }

    stage('test ps') {
      steps {
        sh 'docker ps'
        sh 'curl http://localhost:80'
      }
    }

  }
}