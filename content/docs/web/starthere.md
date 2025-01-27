+++
date = '2025-01-25T10:55:07-08:00'
draft = false
title = 'Start Here'
+++

# Basic Website Setup 

Below is a quick setup guide for building a website with Next.js and Vercel -- Perfect infrastructure to add V0 code to!!

## Project Setup

First check if you have Node:
'''
node -v
'''
If not download [Node](https://nodejs.org/en) and verify with:
'''
node -v
'''
Next create a new web project. This line has some presets that should integrate well with V0 code. 
'''
npx create-next-app@latest project-name --typescript --eslint --tailwind --app --src-dir --import-alias "@/*"
'''
Say no to Turbopack.
Navigate to the project-name directory:
'''
cd project-name
'''
Go to v0, sign up and prompt it to build a website of your choosing.

Try this:
    Click on the add to codebase icon, copy the command and run it in your project root directory (project-name).
    Install the packages and answering the following quesitons like:
    Components.js file - Yes
    Style - Default
    Color - Neutral
    CSS variables = Yes
However there is currently an unfixed [bug](https://github.com/shadcn-ui/ui/issues/6459) with the tech that fetches v0 code so if it dosn't work here is a workaround:
    Manually download the files via zip and copy them over. You don't need to copy everything but many things will be moved.

To test your website locally:
'''
npm run dev
'''
Paste the local host website that if printed to your terminal to test your website.
If you get errors - check if you need to download any extra dependancies and make use of your favorite AI chatbot to resolve them. 

## Pushing to Git
Go to the directory where you want to hold all the code for your cs210 project.
Push your changes to github(for the first time):
'''
git clone https://github.com/your-username/your-repo.git
cd your-repo
git add .
git commit -m "Add project files"
git push
'''

## Deploying on Vercel
Go to Vercel. 
Import your git repository. 
Add any environment variables.
Deploy.

## Documentation 
To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.