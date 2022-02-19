pipeline {
    agent any
    parameters{
        string(name:'ENV',defaultValue:'Test',description:'version to deploy')
        booleanParam(name:'ExecuteTests',defaultValue:true,description:'decide the run to tc')
        choice(name:'APPVERSION',choices:['1.1','1.2','1.3'])
    }
    environment {
        NEW_VERSION = '2.1'
    }
    stages {
        stage('Build') {
            steps {
               script{
                    echo "Buliding the code"
                    echo "Bulid the version ${NEW_VERSION}"
                }
            }
        }
        stage('Test') {
                when{
                    expression{
                        params.ExecuteTests == true
                    }
                }
            steps {
                script{
                    echo"Testing the code"
                }
            }
        }
        stage('Package'){
         input{
             message 'select the version to package'
             ok 'version selected'
             parameters{
                 choice(name:'NEWAPP',choices:['2.1','2.2','2.3'])
             }
         }
            steps{
                script{
                    echo "Packaging the code "
                    echo "Packaging the version:${NEWAPP}"
                }
            }
        }
        stage('Deploy'){
            when{
                expression{
                    BRANCH_NAME == 'dev'
                }
            }
            steps {
                script{
                    echo"Deploying the app"
                    echo "Deploying the app to ENV: ${params.ENV}"      
                    echo "Deploying the app version: ${params.APPVERSION}"             
                }
            }
        }
    }
}