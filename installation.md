# Setting Up SSH Keys for GitHub on macOS

This guide covers the step-by-step process of setting up SSH authentication for GitHub on a Mac.

## Generate SSH Key Pair

1. Open Terminal
2. Generate a new SSH key pair:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
3. When prompted for file location, press Enter to save in default location:
   ```
   Enter file in which to save the key (/Users/YOU/.ssh/id_ed25519):
   ```
4. Optional: Set a passphrase when prompted (recommended for additional security)

## Configure SSH Agent

1. Start the SSH agent:
   ```bash
   eval "$(ssh-agent -s)"
   ```

2. Add your private key to the SSH agent and store in keychain:
   ```bash
   ssh-add --apple-use-keychain ~/.ssh/id_ed25519
   ```

## Add Key to GitHub

1. Copy the public key to clipboard:
   ```bash
   pbcopy < ~/.ssh/id_ed25519.pub
   ```

2. Go to GitHub.com:
   - Click your profile picture → Settings
   - Navigate to "SSH and GPG keys"
   - Click "New SSH key"
   - Add a descriptive title (e.g., "Personal MacBook")
   - Paste the key (Cmd+V)
   - Click "Add SSH key"

## Verify Connection

Test your SSH connection:
```bash
ssh -T git@github.com
```
You should see: "Hi username! You've successfully authenticated with GitHub!"

## Using SSH with Repositories

### For New Repositories:
- When cloning, use the SSH URL (git@github.com:username/repo.git)
- Example:
  ```bash
  git clone git@github.com:username/repo.git
  ```

### For Existing Repositories:
1. Check current remote:
   ```bash
   git remote -v
   ```
2. Update remote to use SSH:
   ```bash
   git remote set-url origin git@github.com:username/repo.git
   ```

## Troubleshooting

If you see permissions errors:
1. Ensure your SSH agent is running:
   ```bash
   eval "$(ssh-agent -s)"
   ```
2. Verify your key is added:
   ```bash
   ssh-add -l
   ```
3. Check GitHub access:
   ```bash
   ssh -vT git@github.com
   ```

## Security Best Practices

1. Never share your private key (`id_ed25519`)
2. Use a strong passphrase when generating the key
3. Keep your SSH key files secure
4. Only add the public key (`id_ed25519.pub`) to GitHub

## Additional Resources

- [GitHub's SSH documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [About SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases)