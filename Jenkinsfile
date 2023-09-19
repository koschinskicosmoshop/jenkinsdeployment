pipeline {
    agent {
        label 'Jenkins-Default'
    }

    environment {
        SERVER_URL = getServerUrl()
        // BRANCH_NAME = master
        // SERVICE_VERSION - sollte übergeben werden?
        // Todo: koschinskicosmoshop => cosmoshop (repo nach owner verschieben)
        SCM_URL = 'https://github.com/koschinskicosmoshop/jenkinsdeployment.git' // SCM=>Source Control Management
    }

    stages {

        stage("SVN Check Local Modifications") {
            steps {
                script {
                    // https rest call
                    restCall('POST', '${SERVER_URL}/todos', '{}')
                }
            }
        }

        stage("Maintenance Mode ON") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }

        stage("Version Switch SVN") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }

        stage("Update Database") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }

        stage("Update Setup Hash") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }

        stage("Increase Version") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }

        stage("Maintenance Mode OFF") {
            steps {
                restCall('POST', '${SERVER_URL}/todos', '{}')
            }
        }
    }
}

def restCall(String method = 'POST',String url,String jsonbody) {
    def response = httpRequest acceptType: 'APPLICATION_JSON', contentType: 'APPLICATION_FORM_DATA',
            requestBody: jsonbody,
            httpMode: method, // timeout: null
            url: url
            // validResponseCodes: '200', validResponseContent: 'OK'
    //echo "Status: ${response.status}"
    //echo "Response: ${response.content}"
    //echo "Headers: ${response.headers}"
}

def getServerUrl() {
    if (JOB_NAME == 'Standard2') {
        return 'https://jsonplaceholder.typicode.com'
    }
    if (JOB_NAME == 'Standard1') {
        return 'http://eco4.cosmoshop.de'
    }
    return ''
}