pipeline {
  triggers {
    cron '''TZ=America/Los_Angeles
H/10 * * * *
'''
  }
  tools {
    maven 'maven-3.9.6'
  }
  agent {
    kubernetes true 
  }
  stages {
    stage('Build_And_Test') {
      environment {
        JAVA_11_PLUS_MAVEN_OPTS = "--add-opens jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.file=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.parser=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.api=ALL-UNNAMED"
        MAVEN_OPTS = "--add-opens jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.file=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.parser=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.tree=ALL-UNNAMED --add-opens jdk.compiler/com.sun.tools.javac.api=ALL-UNNAMED"
      }

      steps {
        sh 'env'
        sh 'mvn -B clean install site -D enable-ci --file pom.xml "-Dsurefire.argLine=--add-opens java.base/java.net=ALL-UNNAMED"'
        junit 'target/**/TEST-*.xml'
      }
    }
  }
}
