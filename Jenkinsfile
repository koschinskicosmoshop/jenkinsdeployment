def SERVERS = [
    Server1: '123.123.123.1',
    Server2: '123.123.123.2',
    Server3: '123.123.123.3'
]

pipeline {
    agent {label 'ubuntu'}

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
            stage("SVN Check Local Modifications") { // ($server)") {
                steps {
                    // https rest call
                    restCall('POST', 'https://...', '{...}')
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
                            restCall('POST', 'https://...', '{...}')
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

def restCall(method,url,jsonbody) {
    def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_FORM_DATA',
            formData: [[body: jsonbody]],
            httpMode: method, quiet: true, responseHandle: 'NONE', timeout: null,
            url: url,
            validResponseCodes: '200', validResponseContent: 'OK'
    println("Status: ${response.status}")
    println("Response: ${response.content}")
    println("Headers: ${response.headers}")
}