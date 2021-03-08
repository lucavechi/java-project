pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
		stage('Check') {
			steps {
				sh 'echo "CWD: "; pwd; ls -la'
				sh 'echo "Previous dir: "; cd ..; pwd; ls -la'
			}
		}
    }
	post {
        always {
            archiveArtifacts artifacts: 'target/*.war', fingerprint: true
        }
    }
}
