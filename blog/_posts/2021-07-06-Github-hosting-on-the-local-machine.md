layout: post
title: How to install PyTorch on the Ubuntu 20.04
comments: true
categories: [ml_py]
tags: Github, host, local machine

### How to set up a Github host on the local machine.

- avoid installing RubyGems packages (called gems) as the root user. Instead, set up a gem installation directory for your user account. The following commands will add environment variables to your ~/.bashrc file to configure the gem installation path:

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

- Install Ruby and other prerequisites:

```
sudo apt-get install ruby-full build-essential zlib1g-dev
gem install jekyll bundler
```

- Finally, install Jekyll and Bundler:

```
gem install jekyll bundler
```
- Create default Jekyll site

```
jekyll new username.github.io
cd username.github.io
bundle install
bundle exec jekyll serve
```
- Check whether the server is operating on http://localhost:4000.