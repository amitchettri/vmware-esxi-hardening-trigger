pipeline{
  agent { label 'master' }
  parameters {
    string(name: 'ServerName', defaultValue: '', description: 'Enter comma separated ESXi Hostname/IP for hardening')
    string(name: 'CredentialID', defaultValue: '', description: 'Enter the credential-id of vSphere server')
  }
  environment{
    git_repo_path = 'https://github.com/rakeshkorukonda2412/vmware-esxi-hardening-trigger.git'
    downstream_build = 'vmware-esxi-hardening'
  }
  stages{
    stage('Trigger downstream builds') {
      steps{
        script{
          def exec_runs = [:]
          ServerName.split(",").each {
            exec_runs["exec_runs${it}"] = {
              build job: "${downstream_build_job_name}",
              parameters: [
                  string(name: 'ServerName', value: "${it}"),
                  string(name: 'CredentialID', value: "${CredentialID}")
              ]
            }
          }
          parallel exec_runs
        }
      }
    }
  }
}
