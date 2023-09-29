<<<<<<< HEAD
# Custom Nginx Modules with Lua
### Version 1.18.0/3cs
Contains All options from official nginx

Contains the following extra nginx and lua 2.1 modules

- [Open Resty Luajit 2.1](https://github.com/3CSDesign/nginx-3cs/tree/main/external/lua-resty-jit#readme)
- [ModSecurity Dynamic Module](https://github.com/3CSDesign/nginx-3cs/tree/main/dynamic/ModSecurity#readme)
- [Nginx Developer Kit Module](https://github.com/3CSDesign/nginx-3cs/tree/main/external/ngx_devel_kit#readme)
- [Open Resty Lua Nginx Dynamic Module](https://github.com/3CSDesign/nginx-3cs/tree/main/external/lua_nginx_module#readme)
- [Open Resty Lua Redis](https://github.com/3CSDesign/nginx-3cs/tree/main/external/lua-resty-redis#readme)
- [Open Resty Lua Core](https://github.com/3CSDesign/nginx-3cs/tree/main/external/lua-resty-core#readme)

## Prerequisites Notes

- [SpiderLabs/ModSecurity installed.](https://github.com/SpiderLabs/ModSecurity)
- Nginx V 1.18.0, if you are not going to install it via this repo

### required packages
- libc6-dev 
- libgd-dev 
- libpcre3-dev 
- iptables 
- perl 
- unzip 
- tar 
- net-tools 
- dnsutils 
- libwww-perl 
- liblwp-protocol-https-perl 
- apt-utils 
- autoconf 
- build-essential  
- git 
- libcurl4-openssl-dev 
- libgeoip-dev 
- liblmdb-dev 
- libpcre++-dev 
- libtool 
- libxml2-dev 
- libyajl-dev 
- pkgconf 
- wget  
- zlib1g-dev

## Installation

### Install openresty lua
```sh 
cd external/lua-resty-jit
make install 
```

### Configure Nginx

```sh
LUAJIT_LIB=/usr/local/bin LUAJIT_INC=/usr/local/include/luajit-2.1 ./configure --add-dynamic-module=dynamic/ModSecurity --add-dynamic-module=external/ngx_devel_kit --add-dynamic-module=external/lua_nginx_module --with-compat
```

### Install Nginx (Optional - skip if you already have Nginx )
```sh
make install
```

### Install Modules
```sh
make modules
```

### Install OpenResty Modules

```sh
cd external/lua-resty-core && make install
cd external/lua-resty-redis && make install
```

### Copy Libs

Depending on how you installed nginx, the modules path might change
Generally installs on /usr/share/nginx/modules/ if you download it via a Package manger
And /usr/local/nginx/modules/ if you install it from this repo

```sh
cp objs/ngx_http_lua_module.so /usr/share/nginx/modules/
cp objs/ndk_http_module.so /usr/share/nginx/modules/
cp objs/ngx_http_modsecurity_module.so /usr/share/nginx/modules
```

### Add lua jit path to /etc/ld.so.conf 
Very Conditional, but this is a suitable method.
```sh
echo "/usr/local/lib" >> /etc/ld.so.conf
```

### Nginx Config
#### Loading the modules
Before event {} block

```conf
load_module modules/ngx_http_modsecurity_module.so;
load_module modules/ndk_http_module.so;
load_module modules/ngx_http_lua_module.so;
```

Inside http {} block

```conf
    modsecurity on;
    modsecurity_rules_file /etc/nginx/modsec/modsec-config.conf;
	lua_package_path "/usr/local/lib/lua/?.lua;;";
```
=======
# uditha-dev3cs
DevOps Practical Test
>>>>>>> a6ed10a18777bb586f7e7eeea1b6242fcb8ffbd4
