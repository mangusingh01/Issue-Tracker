This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.


# GitHub Follow Bot
## 11-28-22
I'm not sure when I'll get around to finishing this tool due to other projects I'm working on. However, I wanted to note that mass following users is against GitHub's TOS (not stated below). Therefore, please use at your own risk!

## Description
This is a GitHub Follow Bot made inside of a Django application. Management of the bot is done inside of Django's default admin center (`/admin`). The bot itself runs in the background of the Django application.

The bot works as the following.

* Runs as a background task in the Django application.
* Management of bot is done in the Django application's web admin center.
* After installing, you must add a super user via Django (e.g. `python3 manage.py createsuperuser`).
* Navigate to the admin web center and add your target user (the user who will be following others) and seeders (users that start out the follow spread).
* After adding the users, add them to the target and seed user list.
* New/least updated users are parsed first up to the max users setting value followed by a random range wait scan time.
* A task is ran in the background for parsed users to make sure they're being followed by target users.
* Another task is ran in the background to retrieve target user's followers and if the Remove Following setting is on, it will automatically unfollow these specific users for the target users.
* Another task is ran that checks all users a target user is following and unfollows the user after *x* days (0 = doesn't unfollow).
* Each follow and unfollow is followed by a random range wait time which may be configured.

## To Do
* Develop a more randomized timing system including most likely active hours of the day.
* See if I can use something better in Django to alter general settings instead of relying on a table in the SQLite database. There are also issues with synchronization due to limitations with Django at this moment. 

## Requirements
The following Python models are required and I'd recommend Python version 3.8 or above since that's what I've tested with.

```
django
aiohttp
```

You can install them like the below.

```bash
# Python < 3
python -m pip install django
python -m pip install aiohttp

pip install django
pip install aiohttp

# Python >= 3
python3 -m pip install django
python3 -m pip install aiohttp

pip3 install django
pip3 install aiohttp
```

## My Motives
A few months ago, I discovered a few GitHub users following over 100K users who were obviously using bots. At first I was shocked because I thought GitHub was against massive following users, but after reading more into it, it appears they don't mind. This had me thinking what if I started following random users as well. Some of these users had a single GitHub.io project that received a lot of attention and I'd assume it's from all the users they were following. I decided to try this. I wanted to see if it'd help me connect with other developers and it certainly did/has! Personally, I haven't used a bot to achieve this, I was actually going through lists of followers from other accounts and following random users. As you'd expect, this completely cluttered my home page, but it also allowed me to discover new projects which was neat in my opinion.

While this is technically 'spam', the good thing I've noticed is it certainly doesn't impact the user I'm following much other than adding a single line in their home page stating I'm following them (or them receiving an email stating this if they have that on). Though, I could see this becoming annoying if many people/bots started doing it (perhaps GitHub could add a user setting that has a maximum following count of a user who can follow them or receive notifications when the user follows).

I actually think it's neat this is allowed so far because it allows others to discover your projects. Since I have quite a few networking projects on this account, I've had some people reach out who I followed stating they found my projects neat because they aren't into that field.

I also wouldn't support empty profiles made just for the purpose of mass following.

## USE AT YOUR OWN RISK
Even though it appears GitHub doesn't mind users massive following others (which I again, support), this is still considered a spam tactic. Therefore, please use this tool at your own risk. I'm not even going to be using it myself because I do enjoy manually following users. I made this project to learn more about Python.

## Settings
Inside of the web interface, a settings model should be visible. The following settings should be inserted.

* **enabled** - Whether to enable the bot or not (should be "1" or "0").
* **max_scan_users** - The maximum users to parse at once before waiting for scan time.
* **wait_time_follow_min** - The minimum number of seconds to wait after following or unfollowing a user.
* **wait_time_follow_max** - The maximum number of seconds to wait after following or unfollowing a user.
* **wait_time_list_min** - The minimum number of seconds to wait after parsing a user's followers page.
* **wait_time_list_max** - The maximum number of seconds to wait after parsing a user's followers page.
* **scan_time_min** - The minimum number of seconds to wait after parsing a batch of users.
* **scan_time_max** - The maximum number of seconds to wait after parsing a batch of users.
* **verbose** - Verbose level for stdout (see levels below).
1. \+ Notification when a target user follows another user.
1. \+ Notification when a target user unfollows a user due to being on the follower list or purge.
1. \+ Notification when users are automatically created from follow spread.
* **user_agent** - The User Agent used to connect to the GitHub API.
* **seed** - Whether to seed (add any existing user's followers to the user list).
* **seed_min_free** - If above 0 and seeding is enabled, seeding will only occur when the amount of new users (users who haven't been followed by any target users) is below this value.
* **max_api_fails** - The max amount of GitHub API fails before stopping the bot for a period of time based off of below (0 = disable).
* **lockout_wait_min** - When the amount of fails exceeds max API fails, it will wait this time minimum in minutes until starting up again.
* **lockout_wait_max** - When the amount of fails exceeds max API fails, it will wait this time maximum in minutes until starting up again.
* **seed_max_pages** - The max amount of pages to seed from with each user parse when looking for new users (seeding).

## Installation
Installation should be performed like a regular Django application. This application uses SQLite as the database. You can read more about Django [here](https://docs.djangoproject.com/en/4.0/intro/tutorial01/). I would recommend the following commands.

```bash
# Make sure Django and aiohttp are installed for this user.

# Clone repository.
git clone https://github.com/gamemann/GitHub-Follower-Bot.git

# Change directory to Django application.
cd GitHub-Follower-Bot/src/github_follower

# Migrate database.
python3 manage.py migrate

# Run the development server on any IP (0.0.0.0) as port 8000.
# NOTE - If you don't want to expose the application publicly, bind it to a LAN IP instead (e.g. 10.50.0.4:8000 instead 0f 0.0.0.0:8000).
python3 manage.py runserver 0.0.0.0:8000

# Create super user for admin web interface.
python3 manage.py createsuperuser
```

The web interface should be located at `http://<host/ip>:<port>`. For example.

http://localhost:8000

While you could technically run the Django application's development server for this bot since only the settings are configured through there, Django recommends reading [this](https://docs.djangoproject.com/en/3.2/howto/deployment/) for production use.

## FAQ
**Why did you choose Django to use as an interface?**

While settings could have been configured on the host itself, I wanted an interface that was easily accessible from anywhere. The best thing for this would be a website in my opinion. Most of my experience is with Django which is why I chose that project.

## Credits
* [Mangu Singh](https://github.com/mangusingh01)

# Library-Management

Website to manage library.


## Tech Stack
### Frontend:
* HTML
* CSS

### Backend+db (preferred):
* Flask
* SQLite

## Components

### Login and Register
User have to register and login first to access the web.

### Issue Book
User can select a book to issue and if the user has enough coins associated to the book, the book will be issued.

### Submit Book
User can submit the book any time and the coins associated to the book will be transfered to the user account which can be used later to issue different books.

### Coin System
Every user is given fix number of coins initially, which can be used to used to get different book. Each book has assiciated with some amount of coins.


## Screenshots

| | |
|:-------------------------:|:-------------------------:|
|<img width="1604" alt="1" src="readme_resources/register.png"> | <img width="1604" alt="2" src="readme_resources/login.png">|
|<img width="1604" alt="4" src="readme_resources/home.png">  |  <img width="1604" alt="5" src="readme_resources/library_page.png">|
|<img width="1604" alt="4" src="readme_resources/book_issue.png">  |  <img width="1604" alt="5" src="readme_resources/after_issue.png">|



## Contributors :trophy:
<p align="center">
<a href="https://github.com/mangusingh01"><img src="https://user-images.githubusercontent.com/58532023/171219272-a68dd897-a9c7-4826-b7e6-10ef84e6a0a8.png" alt="GitHub"/></a>
<a href="https://www.linkedin.com/in/mangu-singh/"><img src="https://user-images.githubusercontent.com/58532023/171219303-8839f911-21bf-453f-b517-9dd6ef9a873c.png" alt="LinkedIn"/></a>
</p>

