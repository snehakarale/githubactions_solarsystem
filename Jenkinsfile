pipeline{
 	agent any
	tool {
		nodejs 'nodejs-24-3-0'
	}
	stages{
		stage("Installign dep"){
			steps{
				sh '''
					node -v
					npm -v
				'''
			}
		}
	}

}
