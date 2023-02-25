---
title: "How This Website Was Made... For Free"
date: 2023-02-25T15:30:46-05:00
summary: "I used Hugo to create this website without coding in HTML/CSS. I used the Blowfish theme and configured Github with Azure for automatic build and deployment. The experience provided valuable insights into Github and Azure capabilities for me."
draft: false
toc: false
images:
categories: ["Website"]
tags: ["Writing", "Hugo", "Tools", "Azure", "Github"]
showAuthor: false
authors:
  - "alanctanner"
---

## Why Hugo and Azure
If you read my [Hello World](/posts/hello-world) post, you know I have thought about setting up a website for a long time. I continuously found myself procrastinating due to the cost of hosting services, server reliability, potential security threats, etc. Also, I did not want to devote hours to writing HTML and CSS, I was mainly aiming to create a professional landing page where I could share what I am currently working on or found interesting with the rest of the world.

When Azure Static Pages became available for preview in 2020, I was inspired to finally construct this website since most of the issues that had previously been holding me back were now resolved by Azure. I was eager to expand my knowledge of cloud platforms, so creating a static website seemed like the ideal opportunity to gain more insight. After reading through all the Azure Static Pages documentation, I eventually decided on Hugo since it had the most attractive themes for the type of site I wanted to create.

## Starting With Hugo
![Hugo Logo](img/hugo-logo-wide.png)
I won't be delving into the details of how to get everything set up and running. Thankfully, Hugo has excellent [documentation](https://gohugo.io/getting-started/quick-start/) that can help you throughout your journey.
Getting Hugo set up is simple 

1.	[Install Hugo](https://gohugo.io/installation/) on your machine (Windows, Mac, or Linux)
2.	[Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3.	create your site with command prompt/terminal
4.	your site will be hosted on your machine locally at localhost:1313

That's it! You now have the fundamental structure and file system to create your own website using Hugo - without having to write a single line of HTML. If you want your website to look just right, then it's ideal that you do some research and find the perfect theme for what you have in mind. While browsing around Hugo's theme directory or Github, you'll be able to find a variety of custom themes from which to choose; depending on the theme, however, configuring them can range in complexity - so make sure that whatever one catches your eye is accompanied by reliable documentation and is properly maintained. I am currently using [Blowfish by Nuno Coração](https://blowfish.page), because its documentation and flexibility are among the best I could find.

## Using Github and Azure for Hosing 
![GithubAndAzureLogs](img/GithubAzure.png)
In the previous section, we installed Git - a convenient and controlled way of making changes. Additionally, by hosting our Hugo configuration on Github, it's possible to utilize actions that will automate building and deploying to Azure for us. When I first set up my website in 2020, it was quite a challenge since Azure Static Pages were still new. Microsoft didn't have many preset features available at the time, so some extra effort had to be put into getting everything functioning properly with various workaround solutions. Thankfully now we're past those difficulties thanks to all the advancements made by Microsoft!

Now it is super simple and Microsoft has great [Getting Started Documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/publish-hugo#deploy-your-web-app). 
1.	create a Static App Resource in Azure
2.	connect your Github account and select the project, and main branch.
3.	Review and Create 
4.	your Hugo site will be built and deployed
5.	Azure will give you a URL to see your built site on the web.

Compared to my experience in the 2020 Preview, this process is so simple with just a few button clicks. Azure does the heavy lifting when it comes to building and deploying your website. Whenever a commit is made on Github's main branch, Azure will automatically build and deploy those changes directly to the web! 

Lastly, you'll likely want to register a domain name for your Azure site. Now that Azure Static Pages is no longer in preview mode, it's easier than ever! You will have a lot of options for registering and setting up the domain, so check out the [Microsoft documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/custom-domain) for detail on the perfect solution for you.
 
## Wrap Up
Overall, setting up my website with Hugo and Azure was a great experience despite all the complexities back when Azure Static Pages were in Preview in 2020. Through this experience, I gained invaluable insight into the capabilities of both Github and Azure. These comprehensive platforms offer a wealth of features to help streamline processes and increase productivity. Finally, I'd encourage everyone to give creating their website too. Crafting and imagining innovative concepts for my website has been an immensely enjoyable experience for me, and it can be for you too. Stay Tuned!

{{< audio src="/audio/BuildWithHugoNarration.mp3" caption="<small>Narration is AI generated with [llElevenLabs](https://beta.elevenlabs.io/)</small>" >}}