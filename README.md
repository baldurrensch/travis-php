travis-php
==========

A set of recipes for using PHP and Travis

## 1. Installing Extensions: 

### 1.1. APC

```yml
before_script: 
    - curl -o APC-3.1.10.tgz http://pecl.php.net/get/APC-3.1.10.tgz
    - tar -xzf APC-3.1.10.tgz
    - sh -c "cd APC-3.1.10 && phpize && ./configure && make && sudo make install && cd .."
    - rm -Rf APC-3.1.10
    - rm APC-3.1.10.tgz
    - echo "extension=apc.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
    - phpenv rehash
```
### 1.2. Memcache

```yml
before_script:
    - echo 'y' | pecl install memcache > ~/memcache.log || ( echo "=== MEMCACHE BUILD FAILED ==="; cat ~/memcache.log )
    - echo "extension=memcache.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
```

### 1.3. Gearman

```yml
before_script:
    - sh -c "sudo apt-get install uuid-dev"
    - curl -L -o libevent-1.4.14b-stable.tar.gz https://github.com/downloads/libevent/libevent/libevent-1.4.14b-stable.tar.gz
    - tar -xzf libevent-1.4.14b-stable.tar.gz
    - sh -c "cd libevent-1.4.14b-stable && ./configure && make && sudo make install && cd .."
    - curl -L -o gearmand-0.14.tar.gz https://launchpad.net/gearmand/1.0/0.14/+download/gearmand-0.14.tar.gz
    - tar -xzf gearmand-0.14.tar.gz
    - sh -c "cd gearmand-0.14 && ./configure && make && sudo make install && cd .."
    - curl -L -o gearman-0.8.3.tgz http://pecl.php.net/get/gearman/0.8.3
    - tar -xzf gearman-0.8.3.tgz
    - sh -c "cd gearman-0.8.3 && phpize && ./configure && make && sudo make install && cd .."
    - echo "extension=gearman.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
```
