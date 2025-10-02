---
layout: post
title: "Setup Guide🚀 for New Windows Students!"
author: David
permalink: /david
---
## Setup Guide🚀 for New Windows Students!
## Week 1-4🔧🔨
Hi Windows Students!!!🎓 You got this!🚀🚀🚀
- We started by creating a Github account and logging into the OpenCodingSociety, a powerful resource where you will use to guide your through for the rest of the year
- Then Accessed VSCode through the offical website, a place where you will code, experiment, and learn, you will be able to program and change your website there
- Then you have to install the VScode on your computer, I will talk about it later
- Then we worked on our About page using vscode.dev 
- Next, we focused on building our tools on VScode
- For Windows students, follow the procedure below 

First, understand the following🚀

Shell Commands
- Windows: wsl, then standard Linux commands inside Ubuntu

Version Control Commands
- git clone: Make a working copy of a git repository from the cloud to your local machine.
- git pull: Update your local copy of the repository with changes from the cloud repository.
- git commit: Save changes to files in your local repository.
- git push: Send updates from your local repository to the remote repository.

Now do the following procedure 

Windows Setup 🚀
Install VSCode
[VSCode link, Select OS and select default on prompts](https://code.visualstudio.com/download)

WSL install ☁️
Open Windows Terminal and Pin to Taskbar. All of these commands are activated from Windows Shell (C:\)

wsl --install -d Ubuntu-24.04
Setup a username and password when prompted. On password you will be typing but will not see respones.

At the conclusion of the install you will receive a WSL Ubuntu prompt. For now we will exit WSL.

exit
Set as default:

wsl --set-default Ubuntu-24.04
To start WSL Ubuntu from (C:\)

wsl
Close Terminal.

WSL Ubuntu Setup
First-time Setup
Open Terminal by right clicking on Terminal in Taskbar and selecting Ubuntu 24.04

Run these commands to set up your Ubuntu developer tools for the first time.

mkdir opencs

cd opencs

git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"

git clone https://github.com/Open-Coding-Society/student.git

cd student/

./scripts/activate_ubuntu.sh # prompts for your recently created WSL Ubuntu password

./scripts/activate.sh # prompts for Git UID and Personal Email

./scripts/venv.sh

System Checks (Optional)
Open Terminal by right clicking on Terminal in Taskbar and selecting Ubuntu 24.04

Run these commands to verify your system setup and check installed tools.

python --version

pip --version

ruby -v

bundle -v

gem --version

git config --global --list

Restarting a terminal

Open Terminal by right clicking on Terminal in Taskbar and selecting Ubuntu 24.04

Each time you open a new terminal session, run these commands to activate your environment and start working on the student project in VS Code.

cd opencs/student

source venv/bin/activate

code .

- Once you are done with all these, Congratulations! You have COMPLETED setting up your basic tools and are ready to start programming!

- HOT TIP🔥🔥🔥 - if you are struggling, ask chatgpt or copilot, they are a great use in solving errors! You can also go ask Mr.Mortensen or others in your group! 

YOU GOT THIS!!! Everything may seem confusing at first, I experienced the confusion at first too! But I didn't give up, I asked Mr.Mortensen and others in my class for help and I gradually understood everything!
