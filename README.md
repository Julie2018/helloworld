# helloworld
import logging
import datetime
import os
import sys
import shutil
import subprocess
import telnetlib
from subprocess import Popen, PIPE, STDOUT
from time import sleep
from os import waitpid, execv, read, write
import paramiko
import time


def main():
    """*Running the test suite(s)*
    """

    # tn = telnetlib.Telnet(HOST)

    ssh = paramiko.SSHClient()
    ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())

    try:
        print ("emma")
        COMMAND = "uname -a"

        try:
            ssh.connect('10.215.0.206', username='root', password='helsinki')
        except paramiko.SSHException:
            print ("Connection Failed")
            quit()

        # ssh = subprocess.Popen(['ssh', 'root@10.74.230.111', COMMAND], stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
        channel = ssh.invoke_shell()

        channel.send('su - stb1\r\n')
        channel.send('whoami\r\n')
        time.sleep(5)
        response = channel.recv(2000)
        print(response)



        # result = ssh.stdout.readlines()
        # if result == []:
        #    error = ssh.stderr.readlines()
        #    print ("ERROR: %s" % error)
        # else:
        #    print (result)

        sys.exit(0)
    except subprocess.CalledProcessError:
        # logging.debug(str(datetime.datetime.now()) + " Failed to upgrade database. Aborting ")
        sys.exit(1)


if __name__ == '__main__':
    main()
 
