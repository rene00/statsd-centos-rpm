statsd-centos-rpm
=================

CentOS/Redhat files that can help you build a statsd RPM using the latest StatsD release (v0.7.0)


Instructions:
```
# NOTE: the first two steps may not be required for statsd
sudo rpm -ivh http://dl.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm
sudo yum install rpm-build rpmdevtools openssl-devel zlib-devel python26
mkdir ~/rpmbuild
cd ~/rpmbuild
rpmdev-setuptree
cp <git repo dir>/spec/statsd.spec ./SPECS/.
cp <git repo dir>/sources/statsd ./SOURCES/statsd-init.d
# you may want to edit config.js before copying it here
cp <git repo dir>/sources/config.js ./SOURCES/config.js
cp <git repo dir>/sources/exampleConfig.js ./SOURCES/exampleConfig.js
cp <git repo dir>/sources/exampleProxyConfig.js ./SOURCES/exampleProxyConfig.js
wget https://github.com/etsy/statsd/archive/v0.7.0.tar.gz -O ./SOURCES/statsd-0.7.0.tar.gz
# NOTE: you may wish to extract the file to ./BUILD/statsd-0.7.0 and then edit ./BUILD/statsd-0.7.0/exampleConfig.js as that file will become the config file used by the RPM after installation
spectool -g -R SPECS/statsd.spec
rpmbuild --clean -ba ./SPECS/statsd.spec
sudo yum install --nogpgcheck RPMS/noarch/statsd-0.7.0-1.noarch.rpm
```
