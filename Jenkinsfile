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
				dependencyCheck additionalArguments: '''--scan \\\'./\\\'
					--out \\\'./\\\'
					--format \\\'ALL\\\'
					--preetyPrint
					''', odcInstallation: 'OWASP-DepCheck-12'
			}
		}
	}

}
