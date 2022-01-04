def label = "test-git-release-${UUID.randomUUID().toString()}"
podTemplate(cloud: 'kubernetes',label: label,imagePullSecrets: [ 'docker-config' ], yaml: """
    apiVersion: v1
    kind: Pod
    spec:
      containers:
      - name: jnlp
        image: registry1.invent.sparkster.me/v4/base/jenkins-jnlp:4.3-8
        tty: true
        imagePullSecrets:
        - name: docker-config
        imagePullPolicy: Always
        args: ['\$(JENKINS_SECRET)', '\$(JENKINS_NAME)']
        resources:
          requests:
            cpu: 8000m
            memory: 8Gi
        env:
        - name: JENKINS_URL
          value: http://jenkins.ci.svc.cluster.local:8080
        - name: NODE_OPTIONS
          value: "--max-old-space-size=8192"
"""
){

node(label){
    environment {
        NEW_VERSION = 'v1.0.0'
    }
    }

        stage('Demo') {
            script {
                git branch: 'master', url: 'https://github.com/jalogut/jenkinsfile-basic-sample.git'
            }
        }
        
         stage('Git_Release') {
            script {
                echo 'Git_Release $(NEW_VERSION)'
            }
        }
    
}
