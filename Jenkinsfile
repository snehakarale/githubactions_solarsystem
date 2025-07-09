pipeline{
 	agent any
	tools {
		nodejs 'nodejs-24-3-0'
	}
	stages{
		stage("Installign dep"){
			steps{
				bat '''
					npm install --no-audit
				'''
			}
		}
		stage("Dep scaning parallel"){
			parallel {
				stage("Npm depedency audit"){
					steps{
						bat '''
							npm audit --audit-level=critical
							echo $?
						'''
					}
				}
				stage("OWASP depCheck"){
					steps{
						dependencyCheck additionalArguments: '''--scan \'./\'
							--out \'./\'
							--format \'ALL\'
							--prettyPrint
							''', odcInstallation: 'OWASP-DepCheck-12'
						dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: true
						junit allowEmptyResults: true, keepProperties: true, testResults: 'dependency-check-junit.xml'
						publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, icon: '', keepAll: true, reportDir: './', reportFiles: 'dependency-check-jenkins.html', reportName: '[Dependency-Check-Jenkins] HTML Report', reportTitles: '', useWrapperFileDirectly: true])
					}
				}
			}
		}
	}

}
