Instructions:
Clone Wintersmith structure, or build in place if that's your thing.
Edit static files on disk.
Run rebuild of Docker image, and redeploy new image to publish changes.

Resulting image is very small, contains no npm binary or node_modules bulk.
This Dockerfile + node + nginx multi build method can be used for many apps, and has great potential for parameterization.
For example one could make a script or simple Jenkins job to rebuild + redeploy the blog. And never have to worry about installing npm on your local machine.

I guess I will make a blog post about it some day.
