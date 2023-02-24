def gv

pipeline {
    agent any
    environment{
        VERSION = '1.0.0'
        SERVER_CREDENTIALS=credentials('docker-hub-cred')
    }
    tools {
        maven  'maven-3.9'
    }
    parameters {
        // string(name:'VERSION', defaultValue: '' , desc : '')
        choice(name:'VERSION', choices:['1.0','1.1'] , description : '')
        booleanParam(name:'executeTest', defaultValue: '' , description : '')
        
    }
    stages {
        stage("build") {
            steps {
                echo "building application ..."
                echo "version of application is ${VERSION}"
                sh 'mvn install'
            }
        }
        stage("test") {
            when {
                expression {
                    BRANCH_NAME = 'dev'
                    params.executeTest
                }
            }
            steps {
                echo "testing application ..."
            }
            
        }  
        stage("build") {
            input {
                message "select the deploying"
                ok "done"
                parameters {
                    // string(name:'VERSION', defaultValue: '' , desc : '')
                    choice(name:'type', choices:['test','deploy'] , description : '')
                }
                
            }
            steps {
                
                echo "deplying application ..."
                echo "mode deployinh is ${type}"
                // echo "credentials is ${SERVER_CREDENTIALS}"
                // sh "${SERVER_CREDENTILAS}"

                // withCredentials([
                //     usernamePasswordCredentails:'docker-hub-cred',usernameVariable: USERNAME , passwordVariable: PASS
                // ]){
                //     sh 'some script ${USERNAME} ${PWD}'
                // }
                echo "version of deploying is ${params.VERSION}"

                
            }
            
        }  
    } 
    //post{
    //    always{

      //  }
        //success{

        //}
         //failed{

        //}
    //} 
}
