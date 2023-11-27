# EC2_CMD-_Connect
When you encounter a "Permission denied (publickey)" error while trying to connect to an EC2 instance through Windows Command Prompt, it typically indicates an issue with the SSH key authentication process. Here are a few possible reasons and solutions:

1. **Incorrect SSH key**: Ensure that you are using the correct SSH key pair for the EC2 instance you are trying to connect to. Double-check that the private key file you are using matches the public key associated with the instance.

2. **Incorrect username**: Make sure you are using the correct username for the EC2 instance. For Amazon Linux 2, the default username is `ec2-user`. For other Linux distributions, such as Ubuntu, the default username is `ubuntu`. If you are connecting to a Windows instance, you should use Remote Desktop (RDP) instead of SSH.

3. **Incorrect file permissions**: The private key file should have restricted permissions to ensure its security. On Windows, you can use the `icacls` command to set the appropriate permissions. For example:
   ```
   icacls private_key.pem /inheritance:r
   icacls private_key.pem /grant:r "%USERNAME%":(R)
   icacls private_key.pem /remove Administrator
   ```

4. **Incorrect key format**: Ensure that the private key file is in the correct format. It should be in OpenSSH format (`.pem` or `.ppk` file) and not in a different format. If you have a key in a different format, you may need to convert it to the correct format using tools like PuTTYgen.

5. **Incorrect SSH configuration**: Check if there are any misconfigurations in your SSH client configuration file (`~/.ssh/config`). Make sure that the host, user, and key file configurations are correct.

6. **Firewall or security group settings**: Verify that the security group associated with the EC2 instance allows SSH (port 22) inbound traffic. Additionally, check if there are any network firewalls or access control lists (ACLs) that might be blocking the connection.

If you have tried these solutions and are still experiencing issues, it may be helpful to review the specific error message and any relevant log files on the EC2 instance for further troubleshooting.
