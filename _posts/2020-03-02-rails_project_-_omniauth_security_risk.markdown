---
layout: post
title:      "Rails Project - OmniAuth Security Risk "
date:       2020-03-02 20:51:47 -0500
permalink:  rails_project_-_omniauth_security_risk
---


TLDR: Use [dotenv gem](https://github.com/bkeepers/dotenv) and do NOT copy and paste your app_key and app_secret in devise.rb and then commit and push to github. If you’re too late, use the help docs to get you out of this sticky situation!

Let me preface this blog post with I made a huge beginner mistake. This is probably not as huge as a big deal I’m making it out to be, but in the future when I’m working for a company or on a team, I can see this being a security threat!

Conceptually, I knew not to post my app_secret to the public when we were learning about session secrets in Sinatra. It’s like a password! You wouldn’t give your bank account password to the whole world, would you?! So tell me WHY I did not realize this during the rails project when implementing Omniauth through Devise. I was told it happens a lot when beginners are learning to code. While comforting, it did not prevent me from spending quite a few hours trying to google how to undo this. 

I thought I was doing great! Following the README directions and copy and pasting from Facebook my app_id and app_secret into the config/initializers/devise.rb file. SUCCESS! I was able to login to my app with my Facebook info. Made commitment and pushed to Github! I continued to work on my project and made additional commits and pushed them to Github. Time to take a pomodoro break and check my email! Then I get this message from a Github bot below and then I realized what I had to undo:

![screenshot-email](https://i.imgur.com/EgSz79P.png)


Well \*\*\*\*.

If you don't want to make the mistake I made, please read along!

First, I would recommend cloning your project to a different folder to have as backup just in case something goes wrong. 
Since I did not want to lose the work I had done in the commits completed after the commit I had treasoned in to my project, and I couldn’t just revert the last commit. I needed to figure out how to just cherrypick the file that I wanted to delete from that specific commit in my public repo. After a couple hours of Google and Stack Overflow loops, I found the [Github help section](https://help.github.com/en/github/authenticating-to-github/removing-sensitive-data-from-a-repository ) as a really helpful resource to undo this mistake. 


Make sure you’re in your repository’s working directory.
1. $ cd YOUR-REPOSITORY
2. Run the following command, replacing PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA with the specific path (not just the filename) you need to take the security issue out of or in *config/initializers/devise.rb* in my case:
    
     ```$ git filter-branch --force --index-filter \ "git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA" \ --prune-empty --tag-name-filter cat -- --all```
    * This will essentially remove the unwanted and compromised file as well as any empty commits generated as a result. Git will process the entire history of every branch and tag, but not check out. It will then overwrite your existing tags.
3. Take out your literal strings of the app_id and app_secret from devise.rb.
![](https://i.imgur.com/D4ALHdM.png)
4. Okay, now how to get Omniauth to work without the literal strings in the config/devise.rb file? 
We are going to use  the dotenv gem! (Shout out to my cohort lead, Jake, and classmate, Mike for walking me through how to use it)
    * $ bundle add 'dotenv-rails'
    * $ touch .env (Make a .env file in the root directory of our project)
    * In the.env file type your app_id and app_secret variables in all caps and assign your actual string app_id and app_secret to them. My example is below:
    * FACEBOOK_ID=YOURAPPID (something like ‘3010281751324’)
FACEBOOK_SECRET=YOURSECRETKEYGOESHERE #(will be something like ‘afew120184htrquja132’)
    * Put your variables in the config/devise.rb file.
    ![code screenshot](https://i.imgur.com/QpNqu9x.png)

5. Immediately type .env in your .gitignore file, so it is not accidentally committed and pushed to Github!
6. Double-check that you've removed all the sensitive data from your repository's history, and that all of your branches are checked out.
7. Once you're happy with it, force-push your local changes to overwrite your GitHub repository, as well as all the branches you've pushed up:
     
     ```$ git push origin --force --all```

8. In order to remove the sensitive file from your tagged releases, you'll also need to force-push against your Git tags:

    ```$ git push origin --force --tags```

9. Check your Github repo to see the magic of your file being corrected, and your app_id and app_secret are safe from public viewing.

I used facebook, but this could happen with any of the omni-auth providers.
Hopefully this guide was helpful if you have found yourself in my same predicament or to prevent you from doing so in the future and save you the headache!

Happy coding!

Mars



