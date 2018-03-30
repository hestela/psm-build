//node('master') {
dockerNode(image: "centos:latest") {
    try {
        stage 'Checkout'
            checkout scm
        stage 'Version Check'
            sh 'cat /etc/os-release'
            sh 'gcc --version'
            sh 'make --version'
        stage 'Fix Build'
            sh 'sed -i "s/uname -p/uname -m/g" buildflags.mak'
            sh 'make clean'
        stage 'Build'
            sh 'make'
        stage 'Install'
            sh 'DESTDIR=`pwd`/install make install'
        currentBuild.result = "SUCCESS"
    } catch (err) {
        currentBuild.result = "FAILURE"
        throw err
    }
}
