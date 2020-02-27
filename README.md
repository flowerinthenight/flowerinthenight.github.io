This is a modified version of [Gaurav Chaurasia's Much-Worse Jekyll theme](https://github.com/gchauras/much-worse-jekyll-theme/).

Source for [https://flowerinthenight.com](https://flowerinthenight.com).

# Environment setup

```bash
$ sudo apt-get install node-js git-core curl zlib1g-dev build-essential libssl-dev \
    libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev \
    libcurl4-openssl-dev python-software-properties libffi-dev ruby-dev

$ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
$ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
$ exec $SHELL

$ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
$ echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
$ exec $SHELL

$ rbenv install 2.3.1
$ rbenv global 2.3.1
$ ruby -v

$ gem install bundler
$ rbenv rehash
```

Then in the root of the project:

```
$ bundle install
```

Host using local server:

```
$ bundle exec jekyll serve --host 0.0.0.0 --port [port]
```

## Troubleshooting
- If build for ruby2.3.1 fails, refer to [https://github.com/rbenv/ruby-build/wiki](https://github.com/rbenv/ruby-build/wiki).
