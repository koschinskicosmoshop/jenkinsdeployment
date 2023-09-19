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

    stages {

        stage("SVN Check Local Modifications") {
            steps {
                echo "Job Name: $JOB_NAME"

                script {
                    // https rest call
                    restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
                }
            }
        }

        stage("Maintenance Mode ON") {
            steps {
                script {
                    restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
                }
            }
        }

        stage("Version Switch SVN") {
            steps {
                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
            }
        }

        stage("Update Database") {
            steps {
                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
            }
        }

        stage("Update Setup Hash") {
            steps {
                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
            }
        }

        stage("Increase Version") {
            steps {
                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
            }
        }

        stage("Maintenance Mode OFF") {
            steps {
                restCall('POST', 'https://jsonplaceholder.typicode.com/todos', '{}')
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