## Wintersmith Docker image!

Clone and build Wintersmith to get started!
Basic instructions and usage can be found at the repo base: https://github.com/jnordberg/wintersmith 

I personally built within a Docker image, then extracted the skeleton build afterwards. I really didn't want to install any dependencies on this system.
But if you don't mind configuring nodejs in your environment, a typical build is fine too.

---

Need to update your blog? Simply edit your content in `static/contents/` per Wintersmith style guide. 

Then, rebuild your Docker image, and deploy the new version!

The resulting Docker image is very small: nginx and static files only on Alpine! No binaries or `node_modules` hanging around.

I will make a blog post about this explaining what else can be done with this template, and how it can be deployed, once I deploy this to my own space online :D

---

Todo: Better Nginx configuration with more examples of usage; right now it is barebones just for static site.

Todo: Script/Dockerfiles showing how to do initial build to get skeleton

Todo: Flesh out .Dockerignore file

Todo: Practice using Markdown...

---
