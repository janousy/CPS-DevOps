node {
    def remote = [:]
    remote.name = "ubuntu"
    remote.host = "160.85.252.170"
    remote.allowAnyHosts = true
    withCredentials([sshUserPrivateKey(credentialsId: 'jenkins', keyFileVariable: 'identity', passphraseVariable: 'pass', usernameVariable: 'user')]){
        remote.user = user
        remote.identityFile = identity
        remote.passphrase = pass
        // stage("Copy Files Over"){
        //     sshPut remote: remote, from: 'C:/Users/Solo de Zaldivar/Documents/HS20/cps/test_scenarios/Master-Thesis-CPS-SORTER/RQ1/Full Road/BeamNG/BeamNG_RF_1_5/beamng_risk_1.5/', into: 'Documents/FuegoGroup/cps/test_scenarios/remoteTests/solodezaldivar'
        // }
        stage("Run cps_sorter on files"){
            sshCommand remote: remote, command: 'source Documents/FuegoGroup/cps/CPS-SORTER/venv/bin/activate\ncps_sorter run-model-eval -i ~/Documents/FuegoGroup/cps/test_scenarios/remoteTests/beamng_risk_1.5 -o ~/Documents/FuegoGroup/cps/test_scenarios/remoteTests/solodezaldivar/output'
        }
        stage("Copy results from remote to local"){
            sshGet remote: remote, from: 'Documents/FuegoGroup/cps/test_scenarios/remoteTests/solodezaldivar/output', into: 'C:/Users/Solo de Zaldivar/Desktop/test/t1', override:true
        }
    }
}