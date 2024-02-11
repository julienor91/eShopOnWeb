pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '/usr/local/share/dotnet/dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            sh '/usr/local/share/dotnet/dotnet test tests/UnitTest'
          }
        }

        stage('Integration') {
          steps {
            sh '/usr/local/share/dotnet/dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh '/usr/local/share/dotnet/dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh '/usr/local/share/dotnet/dotnet publish eShopOnWeb.sln -o /var/aspnet'
      }
    }

  }
}
