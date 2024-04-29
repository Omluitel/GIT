# Setting Up SSH-Based Authentication for Git

1. **Generate SSH Key Pair:**
   Open a terminal or command prompt and use the following command to generate an SSH key pair:
   ```bash
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   Replace `"your_email@example.com"` with your actual email address.

2. **Specify a Filepath and Passphrase (Optional):**
   It will prompt you to specify a filepath to save the key pair. You can press Enter to accept the default location. You can also choose to set a passphrase for added security, though this is optional.

3. **Add the SSH Key to the SSH Agent (Optional but Recommended):**
   Run the following command to add the SSH private key to the SSH agent:
   ```bash
   ssh-add ~/.ssh/id_rsa
   ```
   Replace `~/.ssh/id_rsa` with the path to your private key if you saved it in a different location.

4. **Add Public Key to Git Hosting Service:**
   Log in to your Git hosting service (e.g., GitHub, GitLab, Bitbucket) and navigate to your account settings. Look for the section to add SSH keys. Copy the contents of the public key file (usually `~/.ssh/id_rsa.pub`) and paste it into the SSH key settings on your Git hosting service.

5. **Configure Git to Use SSH:**
   Open your Git configuration file. This file is usually located at `~/.gitconfig` on Unix-like systems. Add or modify the following section:
   ```ini
   [core]
       sshCommand = ssh -i ~/.ssh/id_rsa
   ```
   This tells Git to use the specified SSH private key (`~/.ssh/id_rsa`) for authentication.

6. **Set the Origin for SSH:**
   To set the origin for SSH, navigate to your Git repository directory and run the following command:
   ```bash
   git remote set-url origin git@<git-hosting-service>:<username>/<repository>.git
   ```
   Replace `<git-hosting-service>` with the hostname of your Git hosting service (e.g., github.com), `<username>` with your username on the hosting service, and `<repository>` with the name of your repository.

7. **Test SSH Connection:**
   Test your SSH connection to ensure everything is set up correctly. Run the following command:
   ```bash
   ssh -T git@<git-hosting-service>
   ```
   Replace `<git-hosting-service>` with the hostname of your Git hosting service (e.g., github.com). You should see a message indicating a successful connection.

Now, you should be able to use Git with SSH authentication. When you clone a repository or perform any Git operation that requires authentication, Git will use the SSH key pair you generated.
