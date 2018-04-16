pipeline {
    agent {
        dockerfile {
            filename 'Dockerfile'
        }
    }
    stages {   
        stage('Checkout') {
            steps {
               checkout scm
            }
        }
        stage('Version Check') {
          steps {
            sh 'cat /etc/os-release'
            sh 'gcc --version'
            sh 'make --version'
          }
        }
        stage('Fix Build') {
          steps {
            sh 'sed -i "s/uname -p/uname -m/g" buildflags.mak'
            sh 'make clean'
          }
        }
        stage('Build') {
          steps {
            sh 'make'
          }
        }
        stage('Install') {
          steps {
            sh 'DESTDIR=`pwd`/install make install'
          }
        }  
    }
}
