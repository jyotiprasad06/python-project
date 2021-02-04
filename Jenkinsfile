node('master') {
    stage('Git Checkout') {
    git 'https://github.com/jyotiprasad06/python-project.git'
    }
    stage('Python build') {
        sh 'python3 -m py_compile sources/add2vals.py sources/calc.py' 
        stash(name: 'compiled-results', includes: 'sources/*.py*') 
    }
    stage('Python Test') {
        sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
    }
    stage('Publishing Test Report') {
        junit skipPublishingChecks: true, allowEmptyResults: true, testResults: 'test-reports/results.xml'
    }
}
