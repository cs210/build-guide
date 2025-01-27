+++
date = '2025-01-25T10:55:07-08:00'
draft = false
title = 'Start Here'
+++
# Basic Website Setup  
Below is a quick setup guide for building a website with Next.js and Vercel — the perfect infrastructure to add V0 code to!  

---

## Project Setup  
First, check if you have Node installed. If not, download [Node](https://nodejs.org/en):  
```bash
node -v
```  
Next, create a new web project. The following command includes presets that integrate well with V0 code:  
```bash
npx create-next-app@latest project-name --typescript --eslint --tailwind --app --src-dir --import-alias "@/*"
```  
Say no to Turbopack.  

Navigate to the `project-name` directory:  
```bash
cd project-name
```  

#### Recomended Directory Structure
```
my-app/
├── app/                # Pages and API routes
├── components/         # Reusable UI components
├── lib/               # Utilities and configurations
├── hooks/             # Custom React hooks
├── types/             # TypeScript definitions
└── public/            # Static assets
```
#### Go Build!!
Go to [V0](https://v0.dev/), sign up, and prompt it to build a website of your choosing.  

Try this:  
- Click on the **Add to Codebase** icon, copy the command, and run it in your project root directory (`project-name`).  
- Install the packages and answer the following questions:  
  - **Components.js file**: Yes  
  - **Style**: Default  
  - **Color**: Neutral  
  - **CSS Variables**: Yes  

However, there is currently an unresolved [bug](https://github.com/shadcn-ui/ui/issues/6459) with the tech that fetches V0 code. If it doesn't work, here is a workaround:  
- Manually download the files via zip and copy them over. Only move files that have been updated or added such as the components, hooks, lib and style folders.  

To test your website locally:  
```bash
npm run dev
```  
Paste the local host URL printed in your terminal into your browser to test your website.  

If you get errors, check if you need to download any extra dependencies and make use of your favorite AI chatbot to resolve them.  

---

## Pushing to Git  
Go to the directory where you want to store all the code for your CS210 project.  

Push your changes to GitHub for the first time:  
```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo
git add .
git commit -m "Add project files"
git push
```  

---

## Deploying on Vercel  
- Go to [Vercel](https://vercel.com/)  
- Import your Git repository  
- Add any environment variables  
- Deploy   

---

Ok!! You are now ready to go build the most amazing website of your dreams! Remember to leverage AI tools and dive into documentation when necessary.
 
---

## Documentation  
Want to learn Next.js? The following resources are your best bet:  
- [Next.js Documentation](https://nextjs.org/docs) - Learn about Next.js features and APIs.  
- [Learn Next.js](https://nextjs.org/learn) - An interactive Next.js tutorial.  
- [Vercel Templates](https://vercel.com/templates) - Boilerplate code that can be a great starting point or inspiration for a project or component.
