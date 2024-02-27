pipeline {
    agent any

    stages {
        stage('Job 1: Install and Configure Puppet Agent') {
            steps {
                script {
                    // Specify the SSH credentials to connect to the test server
                    def sshCredentials = '14138f8e-5d28-42d2-894d-23affc985418'

                    // Specify the IP address or hostname of the test server
                    def testServer = '192.168.145.159'

                    // Specify the Puppet Agent installation script
                    def puppetInstallScript = '''
                        #!/bin/bash
                        # Add Puppet repository
                        sudo wget https://apt.puppetlabs.com/puppet6-release-$(lsb_release -sc).deb
                        sudo dpkg -i puppet6-release-$(lsb_release -sc).deb
                        sudo apt-get update

                        # Install Puppet Agent
                        sudo apt-get install -y puppet-agent
                    '''

                    // Use sshagent step to handle SSH authentication
                    sshagent(credentials: [sshCredentials]) {
                        // Execute commands on the remote server
                        sh "ssh ${testServer} '${puppetInstallScript}'"
                        sh "ssh ${testServer} 'sudo /opt/puppetlabs/bin/puppet agent --test'"
                    }
                }
            }
        }
    }
}
