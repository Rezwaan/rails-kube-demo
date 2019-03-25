node {
   stage('Build image') {
  app = docker.build("asia.gcr.io/brave-scanner-234908/rails-kube-demo_app")
}
stage('Push image') {
  docker.withRegistry('https://asia.gcr.io', 'gcr:pace-config-updated') {
    app.push("${env.BUILD_NUMBER}")
    app.push("latest")
  }
}

stage('Deploy App') {
    withKubeConfig([credentialsId: 'pace-config-updated',
                    caCertificate: '-----BEGIN CERTIFICATE-----
MIIDCzCCAfOgAwIBAgIQC9QqhKkkoPvQVmAPug6S/DANBgkqhkiG9w0BAQsFADAv
MS0wKwYDVQQDEyQ5YzYxMGY0Zi1iOWYxLTRiNTgtOTMyMi00MzJkNWI2ZGM5NjQw
HhcNMTkwMzE4MTEzMDQyWhcNMjQwMzE2MTIzMDQyWjAvMS0wKwYDVQQDEyQ5YzYx
MGY0Zi1iOWYxLTRiNTgtOTMyMi00MzJkNWI2ZGM5NjQwggEiMA0GCSqGSIb3DQEB
AQUAA4IBDwAwggEKAoIBAQC1lNrnsk6Mdt3DXVQ7MuTaw4JcuIpf/o9NT0nnq6I5
pLVNvy0Kh+Z6XtSCy0F/i3cczaHAw+ZmtvFA6yZgR0rkd/dJQqyg81OxbTjMqks3
9nL4q0l7wm+9lpcvJ6SKKWHSX6vxiGM60UyHZ95KG8aYO+1F02LP1xTqaFoBdAPZ
SkfTAe+xrFsiSdn2X80MBlWoBEYQttPySCVdsktzJMUIk/fmXrMYrT2+1DYzza8C
bUkrF/pkM4ALgzUTbllsY4SSBt7oKvuBTHdpsopjp1VBNWwOQZTi1ugf9MCujGt6
J85pvT+P0McU+eskPySv/goNkSzi46/GmjGTPf0DH30FAgMBAAGjIzAhMA4GA1Ud
DwEB/wQEAwICBDAPBgNVHRMBAf8EBTADAQH/MA0GCSqGSIb3DQEBCwUAA4IBAQAL
mVBxYsOWC7ZjIX8u59RngopxFDOaIXki+tTC2FbT3MjnmTBWtCrG24YDtO/efAHp
ag49DkN/jukrwue1RChmnKIPQ2+zUMFuGa2OAH+oBPXBhK2Y78cVxP7FhcY5wyW7
f9nmzUc/pYCWCUeUgXPaMr4vC1MxEWc/wKjGinNjd+zfocIQzsXWMA+U/mcBVhiA
NtFrfapEv+gYHacdXxjL13vYGnAXQrseu4VgeEKnDEQcs+y6o//qDAPtAQX0wjgG
aRgV/SNO9w8FiZFlDepmgeglF4CkaH7cVH0BpXjqp4SplV8SuiYP9tpnuk8FEFmq
ITKbbw9X4suY1DUGIA+W
-----END CERTIFICATE-----',
                    serverUrl: 'https://35.194.178.79',
                    //contextName: '<context-name>',
                    //clusterName: '<cluster-name>',
                    namespace: 'default'
                    ]) {
      sh("kubectl apply -f kube/web-deployment.yml")
    }
  }
}
