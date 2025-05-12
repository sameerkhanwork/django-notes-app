@Library("shared") _
pipeline{
    agent {label "sam-agent"}
    
    stages{
        
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        
        stage("Code"){
            steps{
                echo "This is cloning the code"
                git url: "https://github.com/sameerkhanwork/django-notes-app.git", branch: "main"
                echo "Code Cloned Succesfully!!!"
            }
        }
        
        // stage("Code"){
        //     steps{
        //         script{
        //         clone("https://github.com/sameerkhanwork/django-notes-app.git","main")
        //         }
        //     }
        // }
        
        stage("Build"){
            steps{
                echo "This is building the code"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Test"){
            steps{
                echo "This is testing the code"
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "This is pushing the image to DockerHub"
                withCredentials(
                    [usernamePassword(
                        'credentialsId':"DockerHubCred",
                        passwordVariable:"DockerHubPass",
                        usernameVariable:"DockerHubUser")]){
                         sh "docker login -u ${env.DockerHubUser} -p ${env.DockerHubPass}"
                         sh "docker image tag notes-app:latest ${env.DockerHubUser}/notes-app:latest"
                         sh "docker push ${env.DockerHubUser}/notes-app:latest"   
                        }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                // sh "docker run -d -p 8000:8000 notes-app:latest"
                sh "docker compose down -d && docker compose up -d"
            }
        }
    }
}


// @Library('Shared')_
// pipeline{
//     agent { label 'dev-server'}
    
//     stages{
//         stage("Code clone"){
//             steps{
//                 sh "whoami"
//             clone("https://github.com/LondheShubham153/django-notes-app.git","main")
//             }
//         }
//         stage("Code Build"){
//             steps{
//             dockerbuild("notes-app","latest")
//             }
//         }
//         stage("Push to DockerHub"){
//             steps{
//                 dockerpush("dockerHubCreds","notes-app","latest")
//             }
//         }
//         stage("Deploy"){
//             steps{
//                 deploy()
//             }
//         }
        
//     }
// }
