pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/stvake/CW-task4.git', credentialsId: 'token_for_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                // Крок для збірки проекту з Visual Studio
                // Встановіть правильні шляхи до рішення/проекту та параметри MSBuild
                bat 'C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin task4.sln /t:Build /p:Configuration=Release'
            }
        }

        stage('Test') {
            steps {
                // Команди для запуску тестів
                bat "x64\\Release\\task4.exe --gtest_output=xml:x64/Release/task4_report.xml"
            }
        }
    }

    post {
    always {
        // Publish test results using the junit step
         // Specify the path to the XML test result files
		 junit 'x64/Release/task4_report.xml'
    }
}
}