pipeline {
    agent { dockerfile true }
    stages {
	stage('Unit Test'){
	    steps{
 	        sh 'ceedling test:all'
	    }	
	} 
        stage('Static Analysis') {
            steps {
                sh 'cppcheck --xml --xml-version=2 src 2> build/cppcheck.xml'
            }
            post {
                always {
                    publishCppcheck pattern: 'build/cppcheck.xml'
                }
            }
        }
        stage('Target Build') {
            steps {
                sh 'ceedling release_bin'
            }
            post {
                always {
                    archiveArtifacts artifacts: 'build/release/project.axf'
                    archiveArtifacts artifacts: 'build/release/project.bin'
                }
            }
        }
    }
}
