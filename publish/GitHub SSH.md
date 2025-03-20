You can connect to GitHub using the Secure Shell Protocol (SSH), which provides a secure channel over an unsecured network.

#### Set up deploy keys
1. Run the [[How to generate SSH in your local machine?|ssh-key]] on your server, and remember where you save the generated public and private rsa key pair.
2. On GitHub, navigate to the main page of the repository.
3. Under your repository name, click  **Settings**. If you cannot see the "Settings" tab, select the  dropdown menu, then click **Settings**.
4. In the sidebar, click **Deploy Keys**.
5. Click **Add deploy key**.
6. In the "Title" field, provide a title.
7. In the "Key" field, paste your public key.
8. Select **Allow write access** if you want this key to have write access to the repository. A deploy key with write access lets a deployment push to the repository.
9. Click **Add key**.
   
You can test that your local key works by entering `ssh -T git@github.com` in the terminal