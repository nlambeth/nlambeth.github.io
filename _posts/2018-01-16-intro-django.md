---
layout: post
title: "Getting started with Django - Part 1"
---

<!---
Markdown cheatsheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
--->

<!--- Post text follows --->

Working through [the official Django tutorial](https://docs.djangoproject.com/en/2.0/intro/tutorial01/).
I'm working on Cloud9 (the old, good one... not the confusing AWS Cloud9 (Amazon Linux
is weird and scary)). 

1. Check django version: python -m django --version
  - No dice.
2. Check python version: python --version
  - Python 2.7.6
  - We need Python3 for the latest Django.
    - sudo apt update
    - sudo apt install python3.6-venv
3. Create venv and install django:
  - python3.6 -mvenv myvenv
  - source myvenv/bin/activate
  - pip install Django
4. Success. Create a project:
  - django-admin startproject mysite