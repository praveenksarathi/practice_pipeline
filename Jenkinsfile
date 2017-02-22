node ('node') {
        stage 'checkout' {
                checkout scm
        }
        
        stage 'test' {
        env.NODE_ENV = "test"
        print "Environment will be :${env.NODE_ENV}"
        sh 'node -v'
        sh 'npm install'
        sh 'npm test'
        }
        
        stage Build Docker'{
        sh './dockerbuild.sh'
        }
        
        stage 'Deploy'{
        echo 'Push Docker to Repo'
        sh './dockerPushToRepo.sh'
        }
        
        stage 'cleanup'{
        sh 'rm node_modules -rf'
        mail body: 'project build successful',
                 from: 'praveen3.k@aricent.com',
                 replyTo: 'praveen3.k@aricent.com',
                 subject: 'Project build Successful',
                 to: 'praveen3.k@aricent.com'
        }

}
