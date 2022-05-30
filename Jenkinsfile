pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage('Build NodeJsModule') {
      agent {
        docker {
          image 'node:17.1.0-bullseye'
          reuseNode true
        }
      }
      when {
        changeset "**/NoteJsModule/*.*"
        beforeAgent true
      }
      steps {
        dir('NoteJsModule') {
          sh '''
            npm --version
            node --version
            cat frontend.txt
          '''
        }
      }
    }
    stage('Build Java') {
      agent {
        docker {
          image 'maven:3.8.3-openjdk-17'
          reuseNode true
        }
      }
      when {
        changeset "**/ExampleJava/*.*"
        beforeAgent true
      }
      steps {
        dir ('ExampleJava') {
          sh 'mvn --version'
          sh 'mvn test'
        }
      }
    }
//     stage('Build Python') {
//       agent {
//         docker {
//           image ''
//           reuseNode true
//         }
//       }
//       when {
//         changeset "**/pyhtonExample/*.*"
//         beforeAgent true
//       }
//       steps {
//         dir ('backend/api') {
//           sh 'go version'
//           sh 'cat phyton.txt'
//         }
//       }
//     }
  }
}