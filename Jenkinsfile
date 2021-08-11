pipeline {
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'python:3.7' 
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }   
        }

        stage('Test') { 
            agent {
                docker {
                    image 'sureshkvl/pytester' 
                }
            }
            steps {
                sh 'py.test sources/test_calc.py' 
            }
        }
    }
}
