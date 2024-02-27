pipeline {
    agent any

    stages {
        stage('Job 1: Install and Configure Puppet Agent') {
            steps {
                script {
                    // Specify the SSH credentials to connect to the test server
                    def sshCredentials = credentials('your-ssh-credentials-id')

                    // Specify the IP address or hostname of the test server
                    def testServer = 'your-test-server-ip'

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

                    // Copy the Puppet installation script to the test server
                    sshCommand remote: [credentialsId: sshCredentials, user: 'your-ssh-username', host: testServer],
                                command: puppetInstallScript

                    // Configure Puppet Agent
                    sshCommand remote: [credentialsId: sshCredentials, user: 'your-ssh-username', host: testServer],
                                command: 'sudo /opt/puppetlabs/bin/puppet agent --test'
                }
            }
        }
    }
}
