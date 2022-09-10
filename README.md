# To run this code on your computer

> You should have **[Git](https://git-scm.com/downloads)** and **[Node.js](https://nodejs.org/en/download/)**  installed on your computer

> terminal can be cmd/terminal/bash/powershell/etc

1.  Clone this repo and move to project folder, copy-paste command below to your terminal
    ```
    git clone https://github.com/dongumayagay/IMS-4JN
    cd IMS-4JN
    
    ```
3.  Next installing packes.I prefer to insall package using pnpm.

    To install **pnpm**(if you don't have it already install) and to install package that project needs using pnpm

    copy-paste command below to your terminal
    ```
    npm install -g pnpm
    pnpm install
    
    ```
4. create ".env" file on root of your project folder and fillup the variables below from your supabase
   
   VITE_SUPABASE_URL=""
   
   VITE_SUPABASE_ANON_KEY=""
   
    
5. Now that it's ready to run  copy-paste command below to your terminal
    ```
    pnpm run dev
    
    ```
