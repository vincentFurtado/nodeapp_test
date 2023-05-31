node ('any'){
   stage ('Code Pull on Github') {
     git 'https://github.com/vincentFurtado/nodeapp_test.git',
   }

   stage ('Container Image Builds') {
      sh 'sudo docker build -t mugithi/blog:${BUILD_TAG} .'
   }
