statsd-centos-rpm
=================

CentOS/Redhat files that can help you build a statsd RPM.

Instructions:
```
# NOTE: the first two steps may not be required for statsd
sudo rpm -ivh http://dl.fedoraproject.org/pub/epel/5/x86_64/epel-release-5-4.noarch.rpm
sudo yum install rpm-build rpmdevtools openssl-devel zlib-devel python26
mkdir ~/rpmbuild
cd ~/rpmbuild
rpmdev-setuptree
cp <git repo dir>/spec/statsd.spec ./SPECS/.
cp <git repo dir>/init/statsd ./SOURCES/statsd-init.d
spectool -g -R SPECS/statsd.spec
rpmbuild --clean -ba ./SPECS/statsd.spec
sudo yum install RPMS/noarch/statsd-0.6.0-1.noarch.rpm --nogpgcheck
```
