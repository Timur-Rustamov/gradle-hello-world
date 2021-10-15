node('slave1') {
result="OK"
  try {
    stage('checkout'){
    checkout scm
  }
    stage ('build'){
    gradle = tool 'gradle4'
    sh "${gradle}/bin/gradle build"
  }
    stage ('unit test'){
    gradle = tool 'gradle4'
    sh "${gradle}/bin/gradle test"
    }
    stage ('func-test') {
    tests = ["one" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar otoMato 'Hello Otomato!'"},
            "two" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar tsImur 'Hello Tsimur!'"},
            "three" : { sh "sh test-data/int-test.sh build/libs/oto-gradle-1.0.jar rustaMov 'Hello Rustamov!'"}]
    parallel tests
    }
  }
  catch (ex) {
		result="Error"
	}
	stage ('post'){
		if (result == 'OK') {
   			addBadge(icon: 'completed.gif', text: 'OK')
  		}
  		if (result == 'Error') {
   			addBadge(icon: 'error.gif', text: 'Error')
  		} 
      }
	}
