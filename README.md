# hello
#!/bin/bash
# =================================================================================== 配置下载链接hosts ===================================================================================
cp -a /etc/hosts /etc/hosts.ori
echo '' >> /etc/hosts
echo '120.78.139.166            package.dojcyy.xin' >> /etc/hosts

cp -a /etc/profile /etc/profile.ori
echo 'export TMOUT=900' >> /etc/profile

# ==================================================================================== 下载相应安装包 =====================================================================================
cd /usr/local/src
# Nginx安装包
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/pcre-8.34.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/tengine-2.1.1.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/openresty-1.11.2.1.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/openresty-1.11.2.3.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/openresty-1.13.6.1.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/default.conf
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/status.conf
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/nginx.conf

# MySQL安装包
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/mysql-5.6.16.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/my.cnf

# PHP依赖包
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/libiconv-1.14.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/libmcrypt-2.5.8.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/mhash-0.9.9.9.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/mcrypt-2.6.8.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/curl-7.54.1.tar.gz

# PHP安装包
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-5.2.14-fpm-0.5.14.diff.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-5.2.14.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/etc_5.2.14.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-5.4.30.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/etc_5.4.30.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-5.6.20.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/etc_5.6.20.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-7.0.6.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/etc_7.0.6.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php-7.1.7.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/etc_7.1.7.tar.gz

# PHP扩展包
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/phpredis-2.2.5.tgz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/xcache-3.0.3.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/phpredis-php7.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php7_mysql.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/donkeyid-donkeyid-0.7.zip
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/donkeyid-donkeyid-1.0.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/php_ext/swoole-src-master.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/swoole-src-1.9.10.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/swoole-src-2.0.6.tar.gz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/swoole-src-2.0.7.zip
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/mailparse-3.0.2.tgz
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/QConf-1.2.1.tar.gz

# 日志切割脚本
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_nginx.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_php_5214.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_php_5430.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_php_5620.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_php_7006.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/cut_php_7107.sh
wget --user=penghc --password=php@mmc http://package.dojcyy.xin/backup_nginx_conf.sh

# JDK
#wget --user=penghc --password=php@mmc http://package.dojcyy.xin/jdk-8u92-linux-x64.tar.gz


# ====================================================================================== 安装Nginx ========================================================================================
cd /usr/local/src/
# Nginx访问日志
if [ ! -d /media/raid10/logs/nginx ]; then
mkdir -p /media/raid10/logs/nginx
fi

# 站点根路径
if [ ! -d /media/raid10/htdocs ]; then
mkdir -p /media/raid10/htdocs
fi

# 站点备份
if [ ! -d /media/backup/htdocs ]; then
mkdir -p /media/backup/htdocs
fi

# Nginx访问日志备份
if [ ! -d /media/backup/logs/nginx ]; then
mkdir -p /media/backup/logs/nginx
fi

# 安装pcre
cd /usr/local/src/
if [ -f pcre-8.34.tar.gz ]; then
tar -zxf pcre-8.34.tar.gz
cd pcre-8.34
./configure
make
make install
fi

# 添加www账号, 指定gid和uid
id www > /dev/null 2>&1
if [ $? -ne 0 ]; then
groupadd -g 501 www
useradd -g 501 -u 501 www
fi

# 安装Nginx
if [ ! -d /usr/local/webserver/openresty-1.13.6.1 ]; then
cd /usr/local/src/
if [ -f openresty-1.13.6.1.tar.gz ]; then
tar -zxf openresty-1.13.6.1.tar.gz
cd openresty-1.13.6.1
./configure --prefix=/usr/local/webserver/openresty-1.13.6.1 \
--user=www --group=www \
--with-pcre=/usr/local/src/pcre-8.34 \
--with-http_stub_status_module \
--with-http_secure_link_module \
--with-http_sub_module \
--with-http_ssl_module \
--with-luajit
gmake
gmake install


# 链接Nginx安装目录
ln -sv /usr/local/webserver/openresty-1.13.6.1/nginx /usr/local/webserver/nginx

# 配置Nginx全局变量
if [ ! -f /etc/profile.d/openresty-1.13.6.1.sh ]; then
cat > /etc/profile.d/openresty-1.13.6.1.sh << EOF
PATH=/usr/local/webserver/openresty-1.13.6.1/nginx/sbin:/usr/local/webserver/openresty-1.13.6.1/bin:/usr/local/webserver/openresty-1.13.6.1/luajit/bin:\$PATH
EOF
source /etc/profile
fi

# 备份并配置Nginx配置文件
if [ -f /usr/local/src/nginx.conf ]; then
mv /usr/local/webserver/openresty-1.13.6.1/nginx/conf/nginx.conf /usr/local/webserver/openresty-1.13.6.1/nginx/conf/nginx.conf.ori
mv /usr/local/src/nginx.conf /usr/local/webserver/openresty-1.13.6.1/nginx/conf/
fi

# 创建站点配置文件目录
if [ -f /usr/local/src/default.conf ]; then
mkdir -p /usr/local/webserver/nginx/conf/sites
mkdir -p /usr/local/webserver/nginx/conf/sites/zzz_old_config
mv /usr/local/src/default.conf /usr/local/webserver/nginx/conf/sites/
mv /usr/local/src/status.conf /usr/local/webserver/nginx/conf/sites/
ln -sv /usr/local/webserver/nginx/conf/sites /root/sites
fi

# 锁定Nginx主配置文件
chattr +i /usr/local/webserver/openresty-1.13.6.1/nginx/conf/nginx.conf

# 创建Nginx默认站点目录
if [ ! -d /media/raid10/htdocs/default ]; then
chown www.www  /media/raid10/htdocs
mkdir -p /media/raid10/htdocs/default
cp /usr/local/webserver/nginx/html/* /media/raid10/htdocs/default/
fi

# Nginx开机启动
cp -a /etc/rc.local /etc/rc.local.before.nginx
echo "" >> /etc/rc.local
echo "# Start Nginx Service" >> /etc/rc.local
echo "/usr/local/webserver/nginx/sbin/nginx" >> /etc/rc.local


# 删除Nginx安装包
cd /usr/local/src/
rm -rf pcre-8.34
rm -rf openresty-1.13.6.1
fi
fi

# Nginx 日志切割脚本
mkdir -p /media/scripts
mv /usr/local/src/cut_nginx.sh  /media/scripts
echo "# Nginx 日志切割" >> /var/spool/cron/root
echo "00 00 * * * /bin/bash    /media/scripts/cut_nginx.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root

# 临时废弃目录
mkdir -p /media/tmp

# ====================================================================================== 安装MySQL ========================================================================================
# Mysql数据目录
if [ ! -d /media/raid10/mysql_data ]; then
mkdir -p /media/raid10/mysql_data
fi

# Mysql日志目录
if [ ! -d /media/raid10/logs/mysql ]; then
mkdir -p /media/raid10/logs/mysql
fi

# Mysql数据备份目录
if [ ! -d /media/backup/mysql_data ]; then
mkdir -p /media/backup/mysql_data
fi

# Mysql日志备份目录
if [ ! -d /media/backup/logs/mysql ]; then
mkdir -p /media/backup/logs/mysql
fi

# 安装MySQL依赖包
yum install -y cmake git

# 添加MySQL账号, 指定gid和uid
id mysql > /dev/null 2>&1
if [ $? -ne 0 ]; then
groupadd -g 409 mysql
useradd -r -g 409 -s /sbin/nologin mysql
fi

# 安装MySQL
cd /usr/local/src
if [ ! -d /usr/local/webserver/mysql-5.6.16 ]; then
if [ -f mysql-5.6.16.tar.gz ]; then
tar -zxf mysql-5.6.16.tar.gz
cd mysql-5.6.16
cmake -DCMAKE_INSTALL_PREFIX=/usr/local/webserver/mysql-5.6.16 \
-DSYSCONFDIR=/usr/local/webserver/mysql-5.6.16/etc \
-DMYSQL_DATADIR=/media/raid10/mysql_data \
-DMYSQL_TCP_PORT=3306 \
-DMYSQL_UNIX_ADDR=/tmp/mysql.sock \
-DWITH_MYISAM_STORAGE_ENGINE=1 \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_ARCHIVE_STORAGE_ENGINE=1 \
-DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
-DENABLED_LOCAL_INFILE=1 \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DEXTRA_CHARSETS=all
kernel_num=$(cat /proc/cpuinfo | grep "processor" | wc -l)
options="-j$kernel_num"
make $options
make install

# 配置MySQL配置
if [ -f /usr/local/src/my.cnf ]; then
if [ -f /etc/my.cnf ]; then
mv /etc/my.cnf /etc/my.cnf.ori
fi
mkdir /usr/local/webserver/mysql-5.6.16/etc
mv /usr/local/src/my.cnf /usr/local/webserver/mysql-5.6.16/etc/
fi

# 修改MySQL目录权限
chown -R mysql.mysql /usr/local/webserver/mysql-5.6.16
chown -R mysql.mysql /media/raid10/mysql_data
chown -R mysql.mysql /media/raid10/logs/mysql

# 初始化MySQL
ln -sv /usr/local/webserver/mysql-5.6.16/etc/my.cnf /etc/my.cnf
/usr/local/webserver/mysql-5.6.16/scripts/mysql_install_db \
--user=mysql \
--basedir=/usr/local/webserver/mysql-5.6.16 \
--datadir=/media/raid10/mysql_data

# 修改MySQL目录
chown -R root /usr/local/webserver/mysql-5.6.16/

# 锁定MySQL配置文件
chattr +i /usr/local/webserver/mysql-5.6.16/etc/my.cnf

# 链接MySQL安装目录
ln -sv /usr/local/webserver/mysql-5.6.16 /usr/local/webserver/mysql

# 配置MySQL全局变量
if [ ! -f /etc/profile.d/mysql-5.6.16.sh ]; then
cat > /etc/profile.d/mysql-5.6.16.sh << EOF
PATH=\$PATH:/usr/local/webserver/mysql/bin
EOF
source /etc/profile
fi

# 配置MySQL服务脚本
if [ ! -f /etc/init.d/mysqld ]; then
cp support-files/mysql.server /etc/init.d/mysqld
cp -a /etc/init.d/mysqld /etc/init.d/mysqld.ori
chmod 750 /etc/init.d/mysqld
fi

# 开机启动MySQL服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.mysql
echo "" >> /etc/rc.local
echo "# Start Mysql Service" >> /etc/rc.local
echo "#/etc/init.d/mysqld start" >> /etc/rc.local

# 删除MySQL安装包
cd /usr/local/src
rm -rf mysql-5.6.16
fi
fi

# ===================================================================================== 安装PHP依赖包 =====================================================================================
cd /usr/local/src/
if [ -f  libiconv-1.14.tar.gz ]; then
tar -zxf libiconv-1.14.tar.gz
cd libiconv-1.14/
./configure --prefix=/usr/local
make
make install
/sbin/ldconfig

# 删除PHP依赖包
cd /usr/local/src/
rm -rf libiconv-1.14
fi

cd /usr/local/src/
if [ -f libmcrypt-2.5.8.tar.gz ]; then
tar -zxf libmcrypt-2.5.8.tar.gz
cd libmcrypt-2.5.8/
./configure
make
make install

/sbin/ldconfig
cd libltdl/
./configure --enable-ltdl-install
make
make install

ln -sv /usr/local/bin/libmcrypt-config /usr/bin/libmcrypt-config
ln -sv /usr/local/lib/libmcrypt.la /usr/lib/libmcrypt.la
ln -sv /usr/local/lib/libmcrypt.so /usr/lib/libmcrypt.so
ln -sv /usr/local/lib/libmcrypt.so.4 /usr/lib/libmcrypt.so.4
ln -sv /usr/local/lib/libmcrypt.so.4.4.8 /usr/lib/libmcrypt.so.4.4.8

# 删除PHP依赖包
cd /usr/local/src/
rm -rf libmcrypt-2.5.8
fi

cd /usr/local/src/
if [ -f mhash-0.9.9.9.tar.gz ]; then
tar -zxf mhash-0.9.9.9.tar.gz
cd mhash-0.9.9.9/
./configure
make
make install

ln -sv /usr/local/lib/libmhash.a /usr/lib/libmhash.a
ln -sv /usr/local/lib/libmhash.la /usr/lib/libmhash.la
ln -sv /usr/local/lib/libmhash.so /usr/lib/libmhash.so
ln -sv /usr/local/lib/libmhash.so.2 /usr/lib/libmhash.so.2
ln -sv /usr/local/lib/libmhash.so.2.0.1 /usr/lib/libmhash.so.2.0.1

# 删除PHP依赖包
cd /usr/local/src/
rm -rf mhash-0.9.9.9
fi

cd /usr/local/src/
if [ -f mcrypt-2.6.8.tar.gz ]; then
tar -zxf mcrypt-2.6.8.tar.gz
cd mcrypt-2.6.8/
/sbin/ldconfig
export LD_LIBRARY_PATH=/usr/local/lib
./configure
make
make install

# 删除PHP依赖包
cd /usr/local/src/
rm -rf mcrypt-2.6.8
fi

# 安装Curl, 去除NSS支持
cd /usr/local/src/
if [ -f curl-7.54.1.tar.gz ]; then
tar -zxf curl-7.54.1.tar.gz
cd curl-7.54.1/
./configure --prefix=/usr/local/curl-7.54.1 --without-nss
make
make install

cat > /etc/profile.d/curl-7.54.1.sh << EOF
PATH=/usr/local/curl-7.54.1/bin:\$PATH
EOF
source /etc/profile

cat > /etc/ld.so.conf.d/curl-7.54.1.conf << EOF
/usr/local/curl-7.54.1/lib
EOF
ldconfig

# 删除PHP依赖包
cd /usr/local/src/
rm -rf curl-7.54.1
fi

# PHP的xml支持
yum install -y libxml2 libxml2-devel
# PHP的zlib zip bzip2支持
yum install -y zlib zlib-devel bzip2 bzip2-devel bzip2-libs zip unzip gzip
# PHP的图片支持
yum install -y libpng libpng-devel libjpeg libjpeg-devel freetype freetype-devel gd gd-devel

# ===================================================================================== 链接依赖文件 ======================================================================================
if [ ! -f /usr/lib64/libmysqlclient.so.18 ]; then
ln -sv /usr/local/webserver/mysql-5.6.16/lib/libmysqlclient.so.18 /usr/lib64/
fi
if [ ! -f /usr/lib/libmysqlclient.so.18 ]; then
ln -sv /usr/local/webserver/mysql-5.6.16/lib/libmysqlclient.so.18 /usr/lib/
fi
if [ ! -f /usr/local/bin/mysql_config ]; then
ln -sv /usr/local/webserver/mysql-5.6.16/bin/mysql_config         /usr/local/bin/
fi
if [ ! -f /usr/lib/libjpeg.so ]; then
ln -sv /usr/lib64/libjpeg.so /usr/lib/
fi
if [ ! -f /usr/lib/libpng.so ]; then
ln -sv /usr/lib64/libpng.so  /usr/lib/
fi
if [ ! -f /usr/lib/libXpm.so ]; then
ln -sv /usr/lib64/libXpm.so  /usr/lib/
fi
if [ ! -f /usr/lib/libiconv.so.2 ]; then
ln -sv /usr/local/lib/libiconv.so.2 /usr/lib/libiconv.so.2
fi

# =================================================================================== 安装PHP-5.2.14 ======================================================================================
# PHP日志
if [ ! -d /media/raid10/logs/php ]; then
mkdir -p /media/raid10/logs/php
fi
# PHP日志备份
if [ ! -d /media/backup/logs/php ]; then
mkdir -p /media/backup/logs/php
fi

# 安装PHP依赖包
yum install -y patch

# 安装PHP-5.2.14
cd /usr/local/src/
if [ -f php-5.2.14.tar.gz ]; then
tar -zxf php-5.2.14.tar.gz
gzip -cd php-5.2.14-fpm-0.5.14.diff.gz | patch -d php-5.2.14 -p1
cd php-5.2.14
./configure --prefix=/usr/local/webserver/php-5.2.14 \
--with-config-file-path=/usr/local/webserver/php-5.2.14/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-5.2.14/etc/php.d \
--with-mysql=/usr/local/webserver/mysql/ \
--with-mysqli=/usr/local/webserver/mysql/bin/mysql_config \
--with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath \
--enable-bcmath --enable-shmop --enable-sysvsem --with-gettext \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--with-curlwrappers --enable-force-cgi-redirect \
--with-mcrypt --with-mhash --enable-mbstring  \
--enable-pcntl --with-xmlrpc --enable-sockets \
--enable-soap --enable-fastcgi --enable-fpm
make ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-5.2.14服务脚本
cp -a /usr/local/webserver/php-5.2.14/sbin/php-fpm /usr/local/webserver/php-5.2.14/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-5.2.14/sbin/php-fpm
ln -sv /usr/local/webserver/php-5.2.14/sbin/php-fpm /etc/init.d/php-fpm5214

sed -i '56 a\                        chmod 644 /media/raid10/logs/php/error_5214.log' /etc/init.d/php-fpm5214
sed -i '57 a\                        chmod 644 /media/raid10/logs/php/slow_5214.log' /etc/init.d/php-fpm5214
sed -i '118 a\                chmod 644 /media/raid10/logs/php/error_5214.log' /etc/init.d/php-fpm5214
sed -i '119 a\                chmod 644 /media/raid10/logs/php/slow_5214.log' /etc/init.d/php-fpm5214

# 配置PHP-5.2.14配置文件
cd /usr/local/src/
if [ -f etc_5.2.14.tar.gz ]; then
tar -zxf etc_5.2.14.tar.gz
mv /usr/local/webserver/php-5.2.14/etc /usr/local/webserver/php-5.2.14/ori_etc
mv etc_5.2.14 /usr/local/webserver/php-5.2.14/etc
fi

# 开机启动PHP-5.2.14服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.php-5.2.14
echo "" >> /etc/rc.local
echo "# Start PHP 5.2.14 Service" >> /etc/rc.local
echo "#/etc/init.d/php-fpm5214 start" >> /etc/rc.local

# 删除PHP-5.2.14安装包
cd /usr/local/src/
rm -rf php-5.2.14
fi

# 切割 PHP-5.2.14 日志
mv /usr/local/src/cut_php_5214.sh  /media/scripts/
echo "# 切割 PHP-5.2.14 日志" >> /var/spool/cron/root
echo "#00 00 * * * /bin/bash    /media/scripts/cut_php_5214.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root

# =================================================================================== 安装PHP-5.4.30 ======================================================================================
# 安装PHP-5.4.30
cd /usr/local/src/
if [ -f php-5.4.30.tar.gz ]; then
tar -zxf php-5.4.30.tar.gz
cd php-5.4.30
./configure --prefix=/usr/local/webserver/php-5.4.30 \
--with-config-file-path=/usr/local/webserver/php-5.4.30/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-5.4.30/etc/php.d \
--with-mysql=/usr/local/webserver/mysql/ \
--with-mysqli=/usr/local/webserver/mysql/bin/mysql_config \
--with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath \
--enable-bcmath --enable-shmop --enable-sysvsem --with-gettext \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--with-mcrypt --with-mhash --enable-mbstring --enable-sockets --enable-soap \
--enable-fpm --with-fpm-user=www --with-fpm-group=www
kernel_num=$(cat /proc/cpuinfo | grep "processor" | wc -l)
options="-j$kernel_num"
make $options ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-5.4.30服务脚本
cp sapi/fpm/init.d.php-fpm /usr/local/webserver/php-5.4.30/sbin/php-fpm.init
cp -a /usr/local/webserver/php-5.4.30/sbin/php-fpm.init /usr/local/webserver/php-5.4.30/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-5.4.30/sbin/php-fpm.init
ln -sv /usr/local/webserver/php-5.4.30/sbin/php-fpm.init /etc/init.d/php-fpm5430

sed -i '69 a\                        chmod 644 /media/raid10/logs/php/error_5430.log' /etc/init.d/php-fpm5430
sed -i '70 a\                        chmod 644 /media/raid10/logs/php/slow_5430.log' /etc/init.d/php-fpm5430
sed -i '145 a\                chmod 644 /media/raid10/logs/php/error_5430.log' /etc/init.d/php-fpm5430
sed -i '146 a\                chmod 644 /media/raid10/logs/php/slow_5430.log' /etc/init.d/php-fpm5430

# 配置PHP-5.4.30配置文件
cd /usr/local/src/
if [ -f etc_5.4.30.tar.gz ]; then
tar -zxf etc_5.4.30.tar.gz
mv /usr/local/webserver/php-5.4.30/etc /usr/local/webserver/php-5.4.30/ori_etc
mv etc_5.4.30 /usr/local/webserver/php-5.4.30/etc
fi

# 开机启动PHP-5.4.30服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.php-5.4.30
echo "" >> /etc/rc.local
echo "# Start PHP 5.4.30 Service" >> /etc/rc.local
echo "#/etc/init.d/php-fpm5430 start" >> /etc/rc.local

# 删除PHP-5.4.30安装包
cd /usr/local/src/
rm -rf php-5.4.30
fi

# 切割 PHP-5.4.30 日志
mv /usr/local/src/cut_php_5430.sh  /media/scripts/
echo "# 切割 PHP-5.4.30 日志" >> /var/spool/cron/root
echo "00 00 * * * /bin/bash    /media/scripts/cut_php_5430.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root

# =================================================================================== 安装PHP-5.6.20 ======================================================================================
# 安装PHP-5.6.20
cd /usr/local/src/
if [ -f php-5.6.20.tar.gz ]; then
tar -zxf php-5.6.20.tar.gz
cd php-5.6.20
./configure --prefix=/usr/local/webserver/php-5.6.20 \
--with-config-file-path=/usr/local/webserver/php-5.6.20/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-5.6.20/etc/php.d \
--with-mysql --with-mysqli --with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath \
--with-libxml-dir=/usr --enable-bcmath --enable-shmop --enable-sysvsem --with-gettext \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--with-mcrypt --with-mhash --enable-mbstring \
--enable-sockets --enable-soap --with-libdir=lib64 --enable-pcntl --with-xmlrpc \
--enable-fpm --with-fpm-user=www --with-fpm-group=www
kernel_num=$(cat /proc/cpuinfo | grep "processor" | wc -l)
options="-j$kernel_num"
make $options ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-5.6.20服务脚本
cp sapi/fpm/init.d.php-fpm /usr/local/webserver/php-5.6.20/sbin/php-fpm.init
cp -a /usr/local/webserver/php-5.6.20/sbin/php-fpm.init /usr/local/webserver/php-5.6.20/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-5.6.20/sbin/php-fpm.init
ln -sv /usr/local/webserver/php-5.6.20/sbin/php-fpm.init /etc/init.d/php-fpm5620

sed -i '69 a\                        chmod 644 /media/raid10/logs/php/error_5620.log' /etc/init.d/php-fpm5620
sed -i '70 a\                        chmod 644 /media/raid10/logs/php/slow_5620.log' /etc/init.d/php-fpm5620
sed -i '145 a\                chmod 644 /media/raid10/logs/php/error_5620.log' /etc/init.d/php-fpm5620
sed -i '146 a\                chmod 644 /media/raid10/logs/php/slow_5620.log' /etc/init.d/php-fpm5620

# 配置PHP-5.6.20配置文件
cd /usr/local/src/
if [ -f etc_5.6.20.tar.gz ]; then
tar -zxf etc_5.6.20.tar.gz
mv /usr/local/webserver/php-5.6.20/etc /usr/local/webserver/php-5.6.20/ori_etc
mv etc_5.6.20 /usr/local/webserver/php-5.6.20/etc
fi

# 开机启动PHP-5.6.20服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.5.6.20
echo "" >> /etc/rc.local
echo "# Start PHP 5.6.20 Service" >> /etc/rc.local
echo "sysctl vm.nr_hugepages=512" >> /etc/rc.local
echo "#/etc/init.d/php-fpm5620 start" >> /etc/rc.local

# 删除PHP-5.6.20安装包
cd /usr/local/src/
rm -rf php-5.6.20
fi

# 切割 PHP-5.6.20 日志
mv /usr/local/src/cut_php_5620.sh  /media/scripts/
echo "# 切割 PHP-5.6.20 日志" >> /var/spool/cron/root
echo "00 00 * * * /bin/bash    /media/scripts/cut_php_5620.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root

# =================================================================================== 安装PHP-7.0.6 =======================================================================================
# 安装PHP-7.0.6
cd /usr/local/src/
if [ -f php-7.0.6.tar.gz ]; then
tar -zxf php-7.0.6.tar.gz
cd php-7.0.6
./configure --prefix=/usr/local/webserver/php-7.0.6 \
--with-config-file-path=/usr/local/webserver/php-7.0.6/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-7.0.6/etc/php.d \
--with-mysqli=/usr/local/webserver/mysql/bin/mysql_config \
--with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath --enable-pcntl \
--enable-bcmath --enable-shmop --enable-sysvsem --with-gettext \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--with-mcrypt --with-mhash --enable-mbstring --enable-sockets --enable-soap \
--enable-fpm --with-fpm-user=www --with-fpm-group=www
kernel_num=$(cat /proc/cpuinfo | grep "processor" | wc -l)
options="-j$kernel_num"
make $options ZEND_EXTRA_LIBS='-liconv'
#make ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-7.0.6服务脚本
cp sapi/fpm/init.d.php-fpm /usr/local/webserver/php-7.0.6/sbin/php-fpm.init
cp -a /usr/local/webserver/php-7.0.6/sbin/php-fpm.init /usr/local/webserver/php-7.0.6/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-7.0.6/sbin/php-fpm.init
ln -sv /usr/local/webserver/php-7.0.6/sbin/php-fpm.init /etc/init.d/php-fpm7006

sed -i '69 a\                        chmod 644 /media/raid10/logs/php/error_7006.log' /etc/init.d/php-fpm7006
sed -i '70 a\                        chmod 644 /media/raid10/logs/php/slow_7006.log' /etc/init.d/php-fpm7006
sed -i '145 a\                chmod 644 /media/raid10/logs/php/error_7006.log' /etc/init.d/php-fpm7006
sed -i '146 a\                chmod 644 /media/raid10/logs/php/slow_7006.log' /etc/init.d/php-fpm7006

# 配置PHP-7.0.6配置文件
cd /usr/local/src/
if [ -f etc_7.0.6.tar.gz ]; then
tar -zxf etc_7.0.6.tar.gz
mv /usr/local/webserver/php-7.0.6/etc /usr/local/webserver/php-7.0.6/ori_etc
mv etc_7.0.6 /usr/local/webserver/php-7.0.6/etc
fi

# 开机启动PHP-7.0.6服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.php-7.0.6
echo "" >> /etc/rc.local
echo "# Start PHP 7.0.6 Service" >> /etc/rc.local
echo "#/etc/init.d/php-fpm7006 start" >> /etc/rc.local

# 删除PHP-7.0.6安装包
cd /usr/local/src/
rm -rf php-7.0.6
fi

# 切割 PHP-7.0.6 日志
mv /usr/local/src/cut_php_7006.sh  /media/scripts/
echo "# 切割 PHP-7.0.6 日志" >> /var/spool/cron/root
echo "00 00 * * * /bin/bash    /media/scripts/cut_php_7006.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root


# =================================================================================== 安装PHP-7.1.7 =======================================================================================
# 安装PHP-7.1.7
cd /usr/local/src/
if [ -f php-7.1.7.tar.gz ]; then
tar -zxf php-7.1.7.tar.gz
cd php-7.1.7
./configure --prefix=/usr/local/webserver/php-7.1.7 \
--with-config-file-path=/usr/local/webserver/php-7.1.7/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-7.1.7/etc/php.d \
--with-mysqli --with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath --enable-pcntl \
--with-libxml-dir=/usr --enable-bcmath --enable-shmop --enable-sysvsem \
--with-gettext --with-mcrypt --with-mhash --enable-mbstring \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--enable-sockets --enable-soap --with-libdir=lib64 --with-xmlrpc \
--enable-fpm --with-fpm-user=www --with-fpm-group=www
make ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-7.1.7服务脚本
cp sapi/fpm/init.d.php-fpm /usr/local/webserver/php-7.1.7/sbin/php-fpm.init
cp -a /usr/local/webserver/php-7.1.7/sbin/php-fpm.init /usr/local/webserver/php-7.1.7/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-7.1.7/sbin/php-fpm.init
ln -sv /usr/local/webserver/php-7.1.7/sbin/php-fpm.init /etc/init.d/php-fpm7107

sed -i '69 a\                        chmod 644 /media/raid10/logs/php/error_7107.log' /etc/init.d/php-fpm7107
sed -i '70 a\                        chmod 644 /media/raid10/logs/php/slow_7107.log' /etc/init.d/php-fpm7107
sed -i '145 a\                chmod 644 /media/raid10/logs/php/error_7107.log' /etc/init.d/php-fpm7107
sed -i '146 a\                chmod 644 /media/raid10/logs/php/slow_7107.log' /etc/init.d/php-fpm7107

touch /media/raid10/logs/php/error_7107.log /media/raid10/logs/php/slow_7107.log

# 配置PHP-7.1.7配置文件
cd /usr/local/src/
if [ -f etc_7.1.7.tar.gz ]; then
tar -zxf etc_7.1.7.tar.gz
mv /usr/local/webserver/php-7.1.7/etc /usr/local/webserver/php-7.1.7/ori_etc
mv etc_7.1.7 /usr/local/webserver/php-7.1.7/etc
fi

# 开机启动PHP-7.1.7服务, 默认关闭
cp -a /etc/rc.local /etc/rc.local.before.php-7.1.7
echo "" >> /etc/rc.local
echo "# Start PHP 7.1.7 Service" >> /etc/rc.local
echo "#/etc/init.d/php-fpm7107 start" >> /etc/rc.local

# 删除PHP-7.1.7安装包
cd /usr/local/src/
rm -rf php-7.1.7
fi

# 切割 PHP-7.1.7 日志
mv /usr/local/src/cut_php_7107.sh  /media/scripts/
echo "# 切割 PHP-7.1.7 日志" >> /var/spool/cron/root
echo "00 00 * * * /bin/bash    /media/scripts/cut_php_7107.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root
echo "# ====================================================================================================================" >> /var/spool/cron/root

# =================================================================================== 安装PHP-7.1.15 ======================================================================================
tar -zxf php-7.1.15.tar.gz
cd php-7.1.15
./configure --prefix=/usr/local/webserver/php-7.1.15 \
--with-config-file-path=/usr/local/webserver/php-7.1.15/etc \
--with-config-file-scan-dir=/usr/local/webserver/php-7.1.15/etc/php.d \
--with-mysqli --with-pdo-mysql \
--with-openssl --with-curl=/usr/local/curl-7.54.1 --with-zlib --enable-zip --with-bz2 \
--with-iconv-dir=/usr/local --with-xpm-dir=/usr/ --disable-rpath --enable-pcntl \
--with-libxml-dir=/usr --enable-bcmath --enable-shmop --enable-sysvsem \
--with-gettext --with-mcrypt --with-mhash --enable-mbstring \
--with-gd --enable-gd-native-ttf --with-freetype-dir --with-jpeg-dir --with-png-dir \
--enable-sockets --enable-soap --with-libdir=lib64 --with-xmlrpc \
--enable-fpm --with-fpm-user=www --with-fpm-group=www
make ZEND_EXTRA_LIBS='-liconv'
make install

# 配置PHP-7.1.15服务脚本
cp sapi/fpm/init.d.php-fpm /usr/local/webserver/php-7.1.15/sbin/php-fpm.init
cp -a /usr/local/webserver/php-7.1.15/sbin/php-fpm.init /usr/local/webserver/php-7.1.15/sbin/php-fpm.ori
chmod 750 /usr/local/webserver/php-7.1.15/sbin/php-fpm.init
ln -sv /usr/local/webserver/php-7.1.15/sbin/php-fpm.init /etc/init.d/php-fpm7115

sed -i '69 a\                        chmod 644 /media/raid10/logs/php/error_7115.log' /etc/init.d/php-fpm7115
sed -i '70 a\                        chmod 644 /media/raid10/logs/php/slow_7115.log' /etc/init.d/php-fpm7115
sed -i '145 a\                chmod 644 /media/raid10/logs/php/error_7115.log' /etc/init.d/php-fpm7115
sed -i '146 a\                chmod 644 /media/raid10/logs/php/slow_7115.log' /etc/init.d/php-fpm7115

touch /media/raid10/logs/php/error_7115.log /media/raid10/logs/php/slow_7115.log



cp -a php.ini-production  /usr/local/webserver/php-7.1.15/etc/php.ini

cp -a /usr/local/webserver/php-7.1.15/etc/php-fpm.conf.default /usr/local/webserver/php-7.1.15/etc/php-fpm.conf
cp -a /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf.default /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf



sed -i 's#include=/usr/local/webserver/php-7.1.15/etc/php-fpm.d/\*.conf#include=/usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf#'  /usr/local/webserver/php-7.1.15/etc/php-fpm.conf



sed -i 's#\[www\]#\[www-7.1.15\]#' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf


sed -i 's#listen = 127.0.0.1:9000#listen = 127.0.0.1:7115#' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf
sed -i 's#pm = dynamic#pm = static#' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf
sed -i 's#pm.max_children = 5#pm.max_children = 10#' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf
sed -i 's#;slowlog = log/\$pool.log.slow#slowlog = /usr/local/webserver/php-7.1.15/var/log/slow_7115.log#' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf
sed -i 's#;request_slowlog_timeout = 0#request_slowlog_timeout = 2' /usr/local/webserver/php-7.1.15/etc/php-fpm.d/www.conf






cd /usr/local/src/
tar -zxf phpredis-php7.tar.gz
cd phpredis-php7
/usr/local/webserver/php-7.1.15/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.15/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.15/etc/php.ini /usr/local/webserver/php-7.1.15/etc/php.ini.before.redis
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.15/lib/php/extensions/no-debug-non-zts-20160303/redis.so"  /usr/local/webserver/php-7.1.15/etc/php.ini

cd /usr/local/src/
rm -rf phpredis-php7






cd /usr/local/src/
tar -zxf php7_mysql.tar.gz
cd php7_mysql
/usr/local/webserver/php-7.1.15/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.15/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.15/etc/php.ini /usr/local/webserver/php-7.1.15/etc/php.ini.before.mysql
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.15/lib/php/extensions/no-debug-non-zts-20160303/mysql.so"  /usr/local/webserver/php-7.1.15/etc/php.ini

cd /usr/local/src/
rm -rf php7_mysql




cd /usr/local/src/
tar -zxf swoole-src-1.9.10.tar.gz
cd swoole-src-1.9.10
/usr/local/webserver/php-7.1.15/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.15/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.15/etc/php.ini /usr/local/webserver/php-7.1.15/etc/php.ini.before.swoole
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.15/lib/php/extensions/no-debug-non-zts-20160303/swoole.so"  /usr/local/webserver/php-7.1.15/etc/php.ini

cd /usr/local/src/
rm -rf swoole-src-1.9.10










# ================================================================================ 增加默认站点PHP页面 ====================================================================================
# 站点PHP默认首页
if [ ! -f /media/raid10/htdocs/default/prod.php ]; then
cat > /media/raid10/htdocs/default/prod.php << EOF
<center><h1>Nginx</h1></center>
<?php
  phpinfo();
?>
EOF
fi

# 数据库PHP测试页
if [ ! -f /media/raid10/htdocs/default/mysql.php ]; then
cat > /media/raid10/htdocs/default/mysql.php << EOF
<?php
try{
  new PDO('mysql:host=localhost;dbname=test', 'root', '');
  echo "<center><h1>Mysql Connect OK</h1></center>";
}
catch (PDOException \$e){
  echo "<center><h1>Can not connect to this database</h1></center>";
}
?>
EOF
fi

# =================================================================================== 安装composer ========================================================================================
cd /root/
if [ ! -f /usr/local/bin/composer ]; then
#curl -sS https://getcomposer.org/installer | /usr/local/webserver/php-5.6.20/bin/php
/usr/local/webserver/php-5.6.20/bin/php -r "readfile('http://install.phpcomposer.com/installer');" | /usr/local/webserver/php-5.6.20/bin/php
mv composer.phar /usr/local/bin/composer
fi

# ============================================================================= 安装PHP-5.2.14的redis扩展 =================================================================================
cd /usr/local/src/
if [ -f phpredis-2.2.5.tgz ]; then
tar -zxf phpredis-2.2.5.tgz
cd redis-2.2.5
/usr/local/webserver/php-5.2.14/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-5.2.14/bin/php-config
make
make install

cp -a /usr/local/webserver/php-5.2.14/etc/php.ini /usr/local/webserver/php-5.2.14/etc/php.ini.before.redis
sed -i "s@extension_dir = \"./\"@extension_dir = \"/usr/local/webserver/php-5.2.14/lib/php/extensions/no-debug-non-zts-20060613/\"@" /usr/local/webserver/php-5.2.14/etc/php.ini
sed -i "/;extension=php_xsl.dll/ a\extension=redis.so"  /usr/local/webserver/php-5.2.14/etc/php.ini

cd /usr/local/src/
rm -rf redis-2.2.5
fi

# ============================================================================= 安装PHP-5.4.30的redis扩展 =================================================================================
cd /usr/local/src/
if [ -f phpredis-2.2.5.tgz ]; then
tar -zxf phpredis-2.2.5.tgz
cd redis-2.2.5
/usr/local/webserver/php-5.4.30/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-5.4.30/bin/php-config
make
make install

cp -a /usr/local/webserver/php-5.4.30/etc/php.ini /usr/local/webserver/php-5.4.30/etc/php.ini.before.redis
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-5.4.30/lib/php/extensions/no-debug-non-zts-20100525/redis.so"  /usr/local/webserver/php-5.4.30/etc/php.ini

cd /usr/local/src/
rm -rf redis-2.2.5
fi

# ============================================================================= 安装PHP-5.4.30的Xcache扩展 ================================================================================
cd /usr/local/src/
if [ -f xcache-3.0.3.tar.gz ]; then
tar -zxf xcache-3.0.3.tar.gz
cd xcache-3.0.3
/usr/local/webserver/php-5.4.30/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-5.4.30/bin/php-config \
--enable-xcache \
--enable-xcache-coverager \
--enable-xcache-optimizer
make
make install

cp -a /usr/local/webserver/php-5.4.30/etc/php.ini /usr/local/webserver/php-5.4.30/etc/php.ini.before.xcache
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-5.4.30/lib/php/extensions/no-debug-non-zts-20100525/xcache.so"  /usr/local/webserver/php-5.4.30/etc/php.ini

cd /usr/local/src/
rm -rf xcache-3.0.3
fi

# ============================================================================= 安装PHP-5.6.20的redis扩展 =================================================================================
cd /usr/local/src/
if [ -f phpredis-2.2.5.tgz ]; then
tar -zxf phpredis-2.2.5.tgz
cd redis-2.2.5
/usr/local/webserver/php-5.6.20/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-5.6.20/bin/php-config
make
make install

cp -a /usr/local/webserver/php-5.6.20/etc/php.ini /usr/local/webserver/php-5.6.20/etc/php.ini.before.redis
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-5.6.20/lib/php/extensions/no-debug-non-zts-20131226/redis.so"  /usr/local/webserver/php-5.6.20/etc/php.ini

cd /usr/local/src/
rm -rf redis-2.2.5
fi

# ============================================================================= 安装PHP-7.0.6的redis扩展 ==================================================================================
cd /usr/local/src/
if [ -f phpredis-php7.tar.gz ]; then
tar -zxf phpredis-php7.tar.gz
cd phpredis-php7
/usr/local/webserver/php-7.0.6/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.redis
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/redis.so"  /usr/local/webserver/php-7.0.6/etc/php.ini

cd /usr/local/src/
rm -rf phpredis-php7
fi

# ============================================================================= 安装PHP-7.1.7的redis扩展 ==================================================================================
cd /usr/local/src/
if [ -f phpredis-php7.tar.gz ]; then
tar -zxf phpredis-php7.tar.gz
cd phpredis-php7
/usr/local/webserver/php-7.1.7/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.redis
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/redis.so"  /usr/local/webserver/php-7.1.7/etc/php.ini

cd /usr/local/src/
rm -rf phpredis-php7
fi


# =========================================================================== 安装PHP-7.0.6的兼容mysql扩展 ================================================================================
cd /usr/local/src/
if [ -f php7_mysql.tar.gz ]; then
tar -zxf php7_mysql.tar.gz
cd php7_mysql
/usr/local/webserver/php-7.0.6/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.mysql
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/mysql.so"  /usr/local/webserver/php-7.0.6/etc/php.ini

cd /usr/local/src/
rm -rf php7_mysql
fi

# =========================================================================== 安装PHP-7.1.7的兼容mysql扩展 ================================================================================
cd /usr/local/src/
if [ -f php7_mysql.tar.gz ]; then
tar -zxf php7_mysql.tar.gz
cd php7_mysql
/usr/local/webserver/php-7.1.7/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.mysql
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/mysql.so"  /usr/local/webserver/php-7.1.7/etc/php.ini

cd /usr/local/src/
rm -rf php7_mysql
fi

# ========================================================================== 安装PHP-7.0.6的兼容donkeyid扩展 ==============================================================================
cd /usr/local/src/
if [ -f donkeyid-donkeyid-1.0.tar.gz ]; then
tar -zxf donkeyid-donkeyid-1.0.tar.gz
cd donkeyid-donkeyid-1.0/donkeyid
#if [ -f donkeyid-donkeyid-0.7.zip ]; then
#unzip donkeyid-donkeyid-0.7.zip
#cd donkeyid-donkeyid-0.7/donkeyid
/usr/local/webserver/php-7.0.6/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.donkeyid
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/donkeyid.so"  /usr/local/webserver/php-7.0.6/etc/php.ini

cd /usr/local/src/
rm -rf donkeyid-donkeyid-1.0
#rm -rf donkeyid-donkeyid-0.7
fi

# ========================================================================== 安装PHP-7.1.7的兼容donkeyid扩展 ==============================================================================
cd /usr/local/src/
if [ -f donkeyid-donkeyid-1.0.tar.gz ]; then
tar -zxf donkeyid-donkeyid-1.0.tar.gz
cd donkeyid-donkeyid-1.0/donkeyid
#if [ -f donkeyid-donkeyid-0.7.zip ]; then
#unzip donkeyid-donkeyid-0.7.zip
#cd donkeyid-donkeyid-0.7/donkeyid
/usr/local/webserver/php-7.1.7/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.donkeyid
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/donkeyid.so"  /usr/local/webserver/php-7.1.7/etc/php.ini

cd /usr/local/src/
rm -rf donkeyid-donkeyid-1.0
#rm -rf donkeyid-donkeyid-0.7
fi

# =========================================================================== 安装PHP-7.0.6的兼容swoole扩展 ===============================================================================
cd /usr/local/src/
if [ -f swoole-src-1.9.10.tar.gz ]; then
tar -zxf swoole-src-1.9.10.tar.gz
cd swoole-src-1.9.10
/usr/local/webserver/php-7.0.6/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.swoole
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/swoole.so"  /usr/local/webserver/php-7.0.6/etc/php.ini

cd /usr/local/src/
rm -rf swoole-src-1.9.10
fi

# =========================================================================== 安装PHP-7.1.7的兼容swoole扩展 ===============================================================================
cd /usr/local/src/
if [ -f swoole-src-1.9.10.tar.gz ]; then
tar -zxf swoole-src-1.9.10.tar.gz
cd swoole-src-1.9.10
/usr/local/webserver/php-7.1.7/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config
make
make install

cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.swoole
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/swoole.so"  /usr/local/webserver/php-7.1.7/etc/php.ini

cd /usr/local/src/
rm -rf swoole-src-1.9.10
fi


# ========================================================================== 安装PHP-7.0.6的兼容mailparse扩展 =============================================================================
#cd /usr/local/src/
#if [ -f mailparse-3.0.2.tgz ]; then
#tar -zxf mailparse-3.0.2.tgz 
#cd mailparse-3.0.2
#/usr/local/webserver/php-7.0.6/bin/phpize
#./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config
#make
#make install
#
#cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.mailparse
#sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/mailparse.so"  /usr/local/webserver/php-7.0.6/etc/php.ini
#
#cd /usr/local/src/
#rm -rf mailparse-3.0.2
#fi

# ========================================================================== 安装PHP-7.1.7的兼容mailparse扩展 =============================================================================
#cd /usr/local/src/
#if [ -f mailparse-3.0.2.tgz ]; then
#tar -zxf mailparse-3.0.2.tgz 
#cd mailparse-3.0.2
#/usr/local/webserver/php-7.1.7/bin/phpize
#./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config
#make
#make install
#
#cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.mailparse
#sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/mailparse.so"  /usr/local/webserver/php-7.1.7/etc/php.ini
#
#cd /usr/local/src/
#rm -rf mailparse-3.0.2
#fi

# =================================================================================== 安装QConf服务 =======================================================================================
cd /usr/local/src/
if [ -f QConf-1.2.1.tar.gz ]; then
tar -zxf QConf-1.2.1.tar.gz
cd QConf-1.2.1
mkdir build
cd build/
cmake ..
make
make install

# 配置文件
cp -a /usr/local/qconf/conf/idc.conf /usr/local/qconf/conf/idc.conf.ori
sed -i '/127.0.0.1:2181/ i\# 115.29.5.144 - 10.122.69.118' /usr/local/qconf/conf/idc.conf
sed -i 's#127.0.0.1:2181#10.122.69.118:2181#' /usr/local/qconf/conf/idc.conf


fi
# 启动Qconf服务
#sh /usr/local/qconf/bin/agent-cmd.sh start

# ============================================================================ 安装PHP-7.0.6的兼容QConf扩展 ===============================================================================
cd /usr/local/src/QConf-1.2.1/driver/
cp -a php php.ori
cd php
/usr/local/webserver/php-7.0.6/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.0.6/bin/php-config \
--with-libqconf-dir=/usr/local/qconf/include \
--enable-static LDFLAGS=/usr/local/qconf/lib/libqconf.a
make
make install

cp -a /usr/local/webserver/php-7.0.6/etc/php.ini /usr/local/webserver/php-7.0.6/etc/php.ini.before.qconf
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.0.6/lib/php/extensions/no-debug-non-zts-20151012/qconf.so"  /usr/local/webserver/php-7.0.6/etc/php.ini

cd /usr/local/src/QConf-1.2.1/driver/
rm -rf php

# ============================================================================ 安装PHP-7.1.7的兼容QConf扩展 ===============================================================================
cd /usr/local/src/QConf-1.2.1/driver/
cp -a php.ori php
cd php
/usr/local/webserver/php-7.1.7/bin/phpize
./configure --with-php-config=/usr/local/webserver/php-7.1.7/bin/php-config \
--with-libqconf-dir=/usr/local/qconf/include \
--enable-static LDFLAGS=/usr/local/qconf/lib/libqconf.a
make
make install

cp -a /usr/local/webserver/php-7.1.7/etc/php.ini /usr/local/webserver/php-7.1.7/etc/php.ini.before.qconf
sed -i "/;extension=php_xsl.dll/ a\extension=/usr/local/webserver/php-7.1.7/lib/php/extensions/no-debug-non-zts-20160303/qconf.so"  /usr/local/webserver/php-7.1.7/etc/php.ini

cd /usr/local/src/QConf-1.2.1/driver/
rm -rf php

# ================================================================================ 安装PHP各版本及测试 ====================================================================================
/usr/local/webserver/php-5.2.14/bin/php -v
/usr/local/webserver/php-5.4.30/bin/php -v
/usr/local/webserver/php-5.6.20/bin/php -v
/usr/local/webserver/php-7.0.6/bin/php -v
/usr/local/webserver/php-7.1.7/bin/php -v

# 默认环境的PHP版本
cat > /etc/profile.d/php-7.1.7.sh << EOF
PATH=/usr/local/webserver/php-7.1.7/bin:\$PATH
EOF

# 备份 Nginx 配置文件
mv /usr/local/src/backup_nginx_conf.sh  /media/scripts/
echo "# 备份 Nginx 配置文件" >> /var/spool/cron/root
echo "30 00 * * * /bin/bash   /media/scripts/backup_nginx_conf.sh > /dev/null 2>&1" >> /var/spool/cron/root
echo "" >> /var/spool/cron/root
echo "# ====================================== 以下配置业务定时 ============================================================" >> /var/spool/cron/root

# ====================================================================================== TCP回收 ==========================================================================================
cat >> /etc/sysctl.conf << EOF

net.ipv4.tcp_timestamps = 1
net.ipv4.tcp_synack_retries = 1
net.ipv4.tcp_syn_retries = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 1
EOF
sysctl -p


