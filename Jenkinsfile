pipeline {
  agent {
    kubernetes {
      // this label will be the prefix of the generated pod's name
      label 'jenkins-agent-my-app'
      yaml """
apiVersion: v1

kind: Pod

metadata:

  name: command-demo

  labels:

    purpose: demonstrate-command

spec:

  containers:

  - name: command-demo-container

    image: debian

    command: ["printenv"]

    args: ["HOSTNAME", "KUBERNETES_PORT"]

  restartPolicy: OnFailure
"""
    }
  }
  stages {
    stage('Test python') {
      steps {
        container('python') {
          sh "pip install -r requirements.txt"
          sh "python test.py"
        }
      }
    }
  }
}