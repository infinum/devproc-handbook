> *You can see a lot by just looking.*

## Git and GitHub

### What is Git?

Git is a Version Control System (VCS). On a very basic level, there are two awesome things a VCS allows you to do:

* You can track changes in your files
* It simplifies working on files and projects with multiple people

There are multiple Version Control Systems, but Git is by far and large the most popular — both for individual and company use.

You should already have Git installed on your macOS. To check, just run in Terminal:

`git --version`

### What is GitHub?

On the other hand, GitHub is a web-based Git repository (referred to as a remote repository).

* It provides a free and easy place to use Git
* It provides the cloud to store your code in
* It allows you to interact with other developers

There are also other similar services like BitBucket and Gitlab, but in Infinum we are mostly using GitHub.

> **Thou shalt use 2FA everywhere where we use Git!**

## Source code versioning

When using a version control system:

* [Commit early, commit often](https://blog.codinghorror.com/check-in-early-check-in-often/)
* Write your commit notes in the same way you'd write your time tracking log - give a brief description of what you've worked on. This is especially important on those projects where the client has been given access to the repositories. If you are meticulous about your commit notes, you'll be able to use them to track time on Productive.
* Since most of the written communication in the company is in English, please write you commit messages in English.

## SSH keys

Before you start with Git, we encourage you to connect to GitHub or Bitbucket with SSH keys. Using the SSH key, you’ll manage (clone, push, pull..) private repositories without entering your email/username password each time you need to operate on the remote repository.

GitHub has excellent [docs](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh) on SSH, how it is used, how to generate one and connect it with your account. First of all, you need to generate a public/private SSH key pair, then add the public part to GitHub and Bitbucket accounts. To do so on GitHub, follow [these steps](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent), and for Bitbucket [these](https://support.atlassian.com/bitbucket-cloud/docs/add-access-keys/). You can reuse the same SSH key for both GitHub and Bitbucket. To use the SSH key for access, clone the repository using the [SSH clone URL](https://help.github.com/articles/which-remote-url-should-i-use/#cloning-with-ssh).

## .gitconfig

You should set **username** and **email** properties in your `.gitconfig` file, which are then associated with each commit you create. You can set those by executing the following commands:
    
    git config --global user.name "Full Name"
    git config --global user.email "your.mail@infinum.com"

`.gitconfig` is stored inside of your home directory `~/.gitconfig` where you can take a look at how it looks or edit it manually. But those commands above will be sufficient for adding your name and email.
