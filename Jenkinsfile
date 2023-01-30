pipeline{
    agent any 
    tools {
        go '1.19'
    }

 parameters{
    string(name : 'NAME', defaultValue: 'nama-project', description : 'silahkan masukan nama docker')
 }

    stages{
        stage("Build Go Project"){
            steps{
                echo "========executing========"
                sh'go build'
            }
        }
        stage("build container"){
            steps{
                echo "========Build image======"
                sh"docker build -t putrasaut/${params.NAME} ."
        }
    }
        stage("push to DockerHUb"){
            input{
                message "lanjutkan push ke dockerhub?"
                ok "oke"
                submitter "saut"
            }
            steps{
                echo "========Pushing======"
                echo "${env.BUILD_NUMBER}"
                echo "${env.JOB_NAME}"
                echo "${env.TAG_DATE}"
                script {
                   withCredentials([string(credentialsId: 'dockerhubpassword', variable: 'dockerhubpwd')]){
                     sh 'docker login -u putrasaut -p ${dockerhubpwd}'
                    }
                     sh "docker push putrasaut/${params.NAME}"
                }
            }
        }    
    }

    
    post{
    always{
        echo "menjalankan automation"
    }
    success{
        echo "berhasil"
    }
    failure{
        echo "gagal"
    }
    cleanup{
        echo "telah proses selesai"
    }
}
}



