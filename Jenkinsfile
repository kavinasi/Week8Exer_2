podTemplate(yaml: '''
    apiVersion: v1
    kind: Pod
    spec:
      containers:
      - name: gradle
        image: gradle:jdk8
        command:
        - sleep
        args:
        - 99d
      restartPolicy: Never
''') {
  node(POD_LABEL) {
    stage('gradle') {
      git 'https://github.com/kavinasi/Week8.git'
      container('gradle') {

        stage('test calculator') {
          sh '''
          test $(curl calculator-service:8080/sum?a=1\\&b=2) -eq 3
          test $(curl calculator-service:8080/div?a=10\\&b=10) -eq 1

          chmod +x gradlew
          ./gradlew acceptanceTest -D calculator.url=http://calculator-service:8080

          cat build/reports/tests/acceptanceTest/index.html


        '''
        }
      }
    }
  }
}
