---
layout: post
title:  "Travis CI Initial Setup and Problems Encountered"
excerpt: "<p>It kept on complaining about `missing config` whenever I clicked on `More Options > Requests` to check on any builds.</p>"
---

At my previous workplace, we practise Continuous Integration (CI), a development practice which requires developers to integrate code into a shared repository several times a day. The tool that we use constantly is Circle CI. Since I had never integrate any CI tools to my personal projects before, I decided to try out [Travis CI](https://travis-ci.org) that my colleague introduced it to me quite some time ago.

I signed up with their service and allows it to access my github.

![Travis Sign Up](/assets/images/travis/signup.png)

After that, you will be redirected to your profile and in my case it will look like `https://travis-ci.org/profile/ikanyu`. Click to enable the repository you would like travis ci to run.

![Travis Repo](/assets/images/travis/enable_repo.png)

To go to the repo page in travis, click the cog which is between the trigger and my repo name.

Next, I added in a `.travis.yml` to my codebase. I made 2 mistakes when I was doing this step. It kept on complaining about `missing config` whenever I clicked on `More Options > Requests` to check on any builds.

![Config Error](/assets/images/travis/config_error.png)

> Mistake 1: I placed it under `config` file.

Initially I thought it is part of the configuration which is wrong. This must be placed at the most outer layer of hierachy in your code.  

> Mistake 2: I named it with `travis.yml`

Previosly when I worked with cicle ci, the yml file is named as  `circle.yml` so I thought it is applicable to travis yml file as well. After searching around, I found the solution to my problem in [StackOverflow](http://stackoverflow.com/questions/24434434/cant-make-travis-ci-work). Apparently, the file name needs to be names as `.travis.yml`. You need a dot in front of travis.

After pushing my commit once again, I finally could happily see my push building in Travis! 

![Build Success](/assets/images/travis/build_success.png)