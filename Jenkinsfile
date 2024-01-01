
// the commit id is the current image version
def IMAGE_TAG 

// image name 
def IMAGE_NAME = "ahmedmohamed1993/node-web-app"

def myBranchName = "push-docker-image"


def changesetExistsInBranch(branchName) {
    def scm = checkout([$class: 'GitSCM', branches: [[name: "*/${branchName}"]]])
    return scm.GIT_COMMITTER_NAME != null
}

pipeline{
    
    agent any 

    tools {
        nodejs "Node 21.5.0"
    }

    stages{

        stage('Check Changes') {
            steps {
                script {
                    // Check if there are changes in the specific branch (e.g., main)
                    if (changesetExistsInBranch("${myBranchName}")) {
                        currentBuild.result = 'ABORTED'
                        error("No changes in the main branch. Aborting the build.")
                         echo "ho ho ho"
                    }else{
                        echo "hey hey hey"
                    }
                }
            }
        }

        // Init the image tag
        stage("Init image tag") {
            steps{
                script {
                    IMAGE_TAG = load ("main.groovy").lastCommitId()
                }
            }
        }


        // Install dependencies
        stage("Install Dependencies"){
            steps{
                script {
                    sh 'npm install'
                }
            }
        }
        
     

       


    }

}


// // the commit id is the current image version
// def IMAGE_TAG 

// // image name 
// def IMAGE_NAME = "ahmedmohamed1993/node-web-app"


// pipeline{
    
//     agent any 

//     tools {
//         nodejs "Node 21.5.0"
//     }

//     stages{


//         // Init the image tag
//         stage("Init image tag") {
//             steps{
//                 script {
//                     IMAGE_TAG = load ("main.groovy").lastCommitId()
//                 }
//             }
//         }


//         // Install dependencies
//         stage("Install Dependencies"){
//             steps{
//                 script {
//                     sh 'npm install'
//                 }
//             }
//         }
        
//         // Run 
//         stage("Run the app"){
//             steps{
//                 script {
//                     sh '''
//                         node app.js & sleep 1
//                         echo $! > .pidfile
//                         kill $(cat .pidfile)
//                         '''
//                 }
//             }
//         }

//         // Build the docker image
//         stage("Build Docker Image"){
//             steps{
//                 script {
//                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
//                 }
//             }
//         }

//         // Push the image to dockerhub
//         stage("Push the Image to the registry"){
//             steps{
//                 script {
//                        withCredentials(
//                                 [usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]
//                                 ) {
                        
//                                     sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin '
                                
//                                     sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
//                         }
//                 }
//             }

//             post{
//                 always{
//                     echo "Will Delete the image ${IMAGE_NAME}:${IMAGE_TAG}"
//                     sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
//                 }
//             }
//         }

//     }

// }
