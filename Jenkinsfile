node('master') {
    stage('Git Checkout') {
    git branch: 'master', url:'https://github.com/jyotiprasad06/python-project.git'
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
    stage('Archiving Artifacts') {
        sh 'pyinstaller --onefile sources/add2vals.py'
        archiveArtifacts 'dist/add2vals'
    }
    stage('Deploy to PyPi server') {
        twine upload --repository-url http://ec2-18-222-222-169.us-east-2.compute.amazonaws.com:8080 dist/*
    }
}
