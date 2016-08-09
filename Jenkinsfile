node('master') {
    try {
        stage 'Checkout'
            checkout scm
        stage 'Version Check'
            sh 'gcc --version'
            sh 'make --version'
        stage 'Fix Build'
            sh 'sed -i "s/uname -p/uname -m/g" buildflags.mak'
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
