def SERVERS = [
    Server1: '123.123.123.1',
    Server2: '123.123.123.2',
    Server3: '123.123.123.3'
]

pipeline {
    agent {
        label 'Jenkins-Default'
    }

    environment {
        // BRANCH_NAME = master
        // SERVICE_VERSION - sollte übergeben werden?
        // Todo: koschinskicosmoshop => cosmoshop (repo nach owner verschieben)
        SCM_URL = 'https://github.com/koschinskicosmoshop/jenkinsdeployment.git' // SCM=>Source Control Management
    }

    options {
        buildDiscarder(
            logRotator(
                // daysToKeepStr: '7', // history is only kept up to this days
                numToKeepStr: '7', // only this number of build logs are kept
                // artifactDaysToKeepStr: '7', // artifacts are only kept up to this days
                // artifactNumToKeepStr: '7', //  only this number of builds have their artifacts kept
            )
        )
    }

    stages {
        // stage('Github Checkout (all)') {
        //    steps {
        //        git(url: SCM_URL, credentialsId: 'jenkins2_ssh_credentials', branch: '$BRANCH_NAME')
        //    }
        //}

        // SERVERS.each { server, ip ->
            stage("Test Jenkinsfile") { // ($server)") {
                steps {
                    echo "Dies ist eine minimalaufwendige Test-Stage"
                    script {
                        testFunc('Guenter')
                    }
                }
            }

            stage("SVN Check Local Modifications") { // ($server)") {
                steps {
                    script {
                        // https rest call
                        restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
                    }
                }
            }

            stage("Deploy") { // ($server)") {
                // environment {
                //    SERVER_NAME = server
                //    SERVER_IP = ip
                // }
                stages {

                    stage("Maintenance Mode ON") {
                        steps {
                            script {
                                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
                            }
                        }
                    }

                    stage("Version Switch SVN") {
                        steps {
                            restCall('POST', 'https://...', '{...}')
                        }
                    }

                    stage("Update Database") {
                        steps {
                            restCall('POST', 'https://...', '{...}')
                        }
                    }

                    stage("Update Setup Hash") {
                        steps {
                            restCall('POST', 'https://...', '{...}')
                        }
                    }

                    stage("Increase Version") {
                        steps {
                            restCall('POST', 'https://...', '{...}')
                        }
                    }

                    stage("Maintenance Mode OFF") {
                        steps {
                            restCall('POST', 'https://...', '{...}')
                        }
                    }
                }
            }
        //}
    }
}

def testFunc(String msg = 'Platzhalter') {
    echo "Hallo $msg"
}

def restCall(String method = 'POST',String url,String jsonbody) {
    def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_FORM_DATA',
            requestBody: jsonbody,
            httpMode: method, // responseHandle: 'NONE', timeout: null, quiet: true,
            url: url
            // validResponseCodes: '200', validResponseContent: 'OK'
    echo "Status: ${response.status}"
    echo "Response: ${response.content}"
    echo "Headers: ${response.headers}"
}