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
	}

}
