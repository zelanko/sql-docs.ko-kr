---
title: PHP용 드라이버에 대한 Linux 및 macOS 설치
description: 이 지침에서는 Linux 또는 macOS에서 Microsoft Drivers for PHP for SQL Server를 설치하는 방법에 대해 알아봅니다.
ms.date: 11/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
manager: v-mabarw
ms.openlocfilehash: 41b5eaec44c61e03db609bcd81b3e732a2119e7f
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384222"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server의 Linux 및 macOS 설치 자습서
다음 지침은 정리된 환경을 가정하며 Ubuntu 16.04, 18.04 및 20.04, RedHat 7 및 8, Debian 8, 9 및 10, Suse 12 및 15, Alpine 3.11 및 macOS 10.13, 10.14 및 10.15에 PHP 7.x, Microsoft ODBC 드라이버, Apache 웹 서버 및 Microsoft Drivers for PHP for SQL Server를 설치하는 방법을 보여 줍니다. 이 지침에서는 PECL을 사용하여 드라이버를 설치할 것을 권장하지만, [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) GitHub 프로젝트 페이지에서 미리 작성된 이진 파일을 다운로드하고 [Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)의 지침에 따라 설치할 수도 있습니다. 확장 로드에 대한 설명과 php.ini에 확장을 추가하지 않는 이유는 [드라이버 로드](../../connect/php/loading-the-php-sql-driver.md#loading-the-driver-at-php-startup) 섹션을 참조하세요.

이 지침에서는 `pecl install`을 사용하여 기본적으로 PHP 7.4를 설치합니다. `pecl channel-update pecl.php.net`을 먼저 실행해야 할 수 있습니다. 일부 지원되는 Linux 배포판은 기본적으로 PHP 7.1 이하 버전으로 설정되는데 해당 버전은 SQL Server용 PHP 드라이버의 최신 버전에서 지원되지 않습니다. 대신 PHP 7.2 또는 7.3을 설치하려면 각 섹션의 시작 부분에 있는 참고를 참조하세요.

또한 Ubuntu에서 PHP-FPM(PHP FastCGI 프로세스 관리자)를 설치하는 방법에 대한 지침도 포함되어 있습니다. 이 서비스는 Apache 대신 nginx 웹 서버를 사용하는 경우에 필요합니다.

이러한 지침에는 SQLSRV 및 PDO_SQLSRV 드라이버를 모두 설치하는 명령이 포함되어 있지만, 각 드라이버를 독립적으로 설치하고 작동할 수 있습니다. 구성을 사용자 지정하는 데 익숙한 사용자는 SQLSRV 또는 PDO_SQLSRV에 맞게 이러한 지침을 조정할 수 있습니다. 두 드라이버는 아래에 명시된 경우를 제외하고는 동일한 종속성을 갖습니다.

## <a name="contents-of-this-page"></a>이 페이지의 내용

- [Ubuntu 16.04, 18.04, 및 20.04에 드라이버 설치](#installing-the-drivers-on-ubuntu-1604-1804-and-2004)
- [Ubuntu에서 PHP-FPM을 사용하여 드라이버 설치](#installing-the-drivers-with-php-fpm-on-ubuntu)
- [Red Hat 7 및 8에 드라이버 설치](#installing-the-drivers-on-red-hat-7-and-8)
- [Debian 8, 9 및 10에 드라이버 설치](#installing-the-drivers-on-debian-8-9-and-10)
- [Suse 12 및 15에 드라이버 설치](#installing-the-drivers-on-suse-12-and-15)
- [Alpine 3.11에 드라이버 설치](#installing-the-drivers-on-alpine-311)
- [macOS High Sierra, Mojave 및 Catalina에 드라이버 설치](#installing-the-drivers-on-macos-high-sierra-mojave-and-catalina)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-2004"></a>Ubuntu 16.04, 18.04, 및 20.04에 드라이버 설치

> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 7.4를 7.2 또는 7.3으로 바꿉니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Ubuntu용 ODBC 드라이버를 설치합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

시스템에 PHP 버전이 하나만 있는 경우 마지막 단계를 `phpenmod sqlsrv pdo_sqlsrv`로 간소화할 수 있습니다.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache 설치 및 드라이버 로드 구성
```bash
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo service apache2 restart
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="installing-the-drivers-with-php-fpm-on-ubuntu"></a>Ubuntu에서 PHP-FPM을 사용하여 드라이버 설치

> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 7.4를 7.2 또는 7.3으로 바꿉니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml php7.4-fpm -y --allow-unauthenticated
```
실행하여 PHP FPM 서비스의 상태를 확인
```bash
systemctl status php7.4-fpm
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Ubuntu용 ODBC 드라이버를 설치합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl config-set php_ini /etc/php/7.4/fpm/php.ini
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```
시스템에 PHP 버전이 하나만 있는 경우 마지막 단계를 `phpenmod sqlsrv pdo_sqlsrv`로 간소화할 수 있습니다.

`sqlsrv.ini` 및 `pdo_sqlsrv.ini`가 `/etc/php/7.4/fpm/conf.d/`에 있는지 확인합니다.
```bash
ls /etc/php/7.4/fpm/conf.d/*sqlsrv.ini
```
PHP FPM 서비스를 다시 시작합니다.
```bash
sudo systemctl restart php7.4-fpm
```

### <a name="step-4-install-and-configure-nginx"></a>4단계. nginx 설치 및 구성
```bash
sudo apt-get update
sudo apt-get install nginx
sudo systemctl status nginx
```
nginx를 구성하려면 `/etc/nginx/sites-available/default` 파일을 편집해야 합니다. `# Add index.php to the list if you are using PHP`라고 표시되는 섹션 아래 목록에 `index.php`를 추가합니다.
```
# Add index.php to the list if you are using PHP
index index.html index.htm index.nginx-debian.html index.php;
```
다음으로 `# pass PHP scripts to FastCGI server` 섹션을 다음과 같이 수정합니다.
```
# pass PHP scripts to FastCGI server
#
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
}
```
### <a name="step-5-restart-nginx-and-test-the-sample-script"></a>5단계. nginx 다시 시작 및 샘플 스크립트 테스트
```bash
sudo systemctl restart nginx.service
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="installing-the-drivers-on-red-hat-7-and-8"></a>Red Hat 7 및 8에 드라이버 설치

### <a name="step-1-install-php"></a>1단계. PHP 설치

Red Hat 7에 PHP를 설치하려면 다음을 실행합니다.
> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 remi-php74를 remi-php72 또는 remi-php73으로 각각 바꿉니다.
```bash
sudo su
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php74
yum update
# Note: The php-pdo package is required only for the PDO_SQLSRV driver
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```

Red Hat 8에 PHP를 설치하려면 다음을 실행합니다.
> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 remi-7.4를 remi-7.2 또는 remi-7.3으로 바꿉니다.
```bash
sudo su
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf install yum-utils
dnf module reset php
dnf module install php:remi-7.4
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
dnf update
# Note: The php-pdo package is required only for the PDO_SQLSRV driver
dnf install php-pdo php-pear php-devel
```

### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Red Hat 7 또는 8용 ODBC 드라이버를 설치합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```

또는 다음과 같이 Remi 리포지토리에서 설치할 수 있습니다.
```bash
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>4단계. Apache 설치
```bash
sudo yum install httpd
```
기본적으로 SELinux가 설치되고 적용 모드로 실행됩니다. SELinux를 통한 Apache의 데이터베이스 연결을 허용하려면 다음 명령을 실행합니다.
```bash
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo apachectl restart
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="installing-the-drivers-on-debian-8-9-and-10"></a>Debian 8, 9 및 10에 드라이버 설치

> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 7.4를 7.2 또는 7.3으로 바꿉니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```bash
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.4 php7.4-dev php7.4-xml php7.4-intl
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Debian용 ODBC 드라이버를 설치합니다. 

브라우저에서 올바르게 표시되는 PHP 출력을 얻기 위해 올바른 로캘을 생성해야 할 수도 있습니다. 예를 들어 en_US UTF-8 로캘의 경우 다음 명령을 실행합니다.
```bash
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```
`/usr/sbin`를 `$PATH`에 추가해야 할 수 있습니다. 여기에 `locale-gen` 실행 파일이 있기 때문입니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

시스템에 PHP 버전이 하나만 있는 경우 마지막 단계를 `phpenmod sqlsrv pdo_sqlsrv`로 간소화할 수 있습니다. `locale-gen`과 마찬가지로 `phpenmod`는 `/usr/sbin`에 있으므로 이 디렉터리를 `$PATH`에 추가해야 할 수 있습니다.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache 설치 및 드라이버 로드 구성
```bash
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo service apache2 restart
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Suse 12 및 15에 드라이버 설치

> [!NOTE]
> 다음 지침에서 `<SuseVersion>`을 사용 중인 Suse 버전으로 바꿉니다. Suse Enterprise Linux 15를 사용하는 경우 SLE_15 또는 SLE_15_SP1이 됩니다. Suse 12의 경우 SLE_12_SP4(해당하는 경우 그 이상)를 사용합니다. 모든 버전의 Suse Linux에서 모든 버전의 PHP를 사용할 수 있는 것은 아닙니다. 기본 버전 PHP를 사용할 수 있는 Suse 버전을 확인하려면 `http://download.opensuse.org/repositories/devel:/languages:/php`를 참조하고, Suse 버전에 사용할 수 있는 다른 버전의 PHP를 확인하려면 `http://download.opensuse.org/repositories/devel:/languages:/php:/`를 참조하세요.

> [!NOTE]
> Suse 12용 PHP 7.4 패키지는 없습니다. PHP 7.2를 설치하려면 아래 리포지토리 URL을 다음 URL로 바꿉니다. `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`
> PHP 7.3을 설치하려면 아래 리포지토리 URL을 다음 URL로 바꿉니다. `https://download.opensuse.org/repositories/devel:/languages:/php:/php73/<SuseVersion>/devel:languages:php:php73.repo`

### <a name="step-1-install-php"></a>1단계. PHP 설치
```bash
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Suse용 ODBC 드라이버를 설치합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
> [!NOTE]
> `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`이라는 오류 메시지가 표시되면, /usr/bin/pecl에 있는 pecl 스크립트를 편집하고 마지막 줄에서 `-n` 스위치를 제거합니다. 이 스위치가 있으면 PHP를 호출할 때 PECL에서 ini 파일을 로드할 수 없어 OpenSSL 확장이 로드되지 않습니다.

```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache 설치 및 드라이버 로드 구성
```bash
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo systemctl restart apache2
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="installing-the-drivers-on-alpine-311"></a>Alpine 3.11에 드라이버 설치

> [!NOTE]
> PHP의 기본 버전은 7.3입니다. 다른 PHP 버전은 다른 Alpine 3.11용 리포지토리에서 사용할 수 있습니다. 대신, PHP를 원본에서 컴파일할 수 있습니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
Alpine 용 PHP 패키지는 `edge/community` 리포지토리에서 찾을 수 있습니다. WIKI 페이지에서 [커뮤니티 리포지토리 사용](https://wiki.alpinelinux.org/wiki/Enable_Community_Repository)을 확인합니다. `/etc/apt/repositories`에 다음 줄을 추가하여 `<mirror>`를 Alpine 리포지토리 미러의 URL로 바꿉니다.
```
http://<mirror>/alpine/edge/community
```
다음을 실행합니다.
```bash
sudo su
apk update
# Note: The php7-pdo package is required only for the PDO_SQLSRV driver
apk add php7 php7-dev php7-pear php7-pdo php7-openssl autoconf make g++
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[Linux 설치 문서](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)의 지침에 따라 Alpine용 ODBC 드라이버를 설치합니다. 

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/00_sqlsrv.ini
```

### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache 설치 및 드라이버 로드 구성
```bash
sudo apk add php7-apache2 apache2
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo rc-service apache2 restart
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.


## <a name="installing-the-drivers-on-macos-high-sierra-mojave-and-catalina"></a>macOS High Sierra, Mojave 및 Catalina에 드라이버 설치

brew가 아직 없는 경우 다음과 같이 설치합니다.
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> PHP 7.2 또는 7.3을 설치하려면 다음 명령에서 php@7.4를 php@7.2 또는 php@7.3으로 각각 바꿉니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치

```bash
brew tap
brew tap homebrew/core
brew install php@7.4
```
이제 PHP가 경로에 있어야 합니다. `php -v`를 실행하여 올바른 버전의 PHP를 실행하고 있는지 확인합니다. PHP가 경로에 없거나 올바른 버전이 아닌 경우 다음을 실행합니다.
```bash
brew link --force --overwrite php@7.4
```

### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
[macOS 설치 문서](../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)의 지침에 따라 macOS용 ODBC 드라이버를 설치합니다. 

GNU Make 도구를 설치해야 할 수도 있습니다.
```bash
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server용 PHP 드라이버 설치
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache 설치 및 드라이버 로드 구성
```bash
brew install apache2
```
현재 Apache 설치에 대한 Apache 구성 파일 `httpd.conf`를 찾으려면 다음을 실행합니다. 
```bash
/usr/local/bin/apachectl -V | grep SERVER_CONFIG_FILE
``` 
다음 명령은 `httpd.conf`에 필요한 구성을 추가합니다. `/usr/local/etc/httpd/httpd.conf`를 이전 명령에서 반환된 경로로 대체해야 합니다.
```bash
echo "LoadModule php7_module /usr/local/opt/php@7.4/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 및 샘플 스크립트 테스트
```bash
sudo apachectl restart
```
설치를 테스트하려면 이 문서의 끝에 있는 [설치 테스트](#testing-your-installation)를 참조하세요.

## <a name="testing-your-installation"></a>설치 테스트

이 샘플 스크립트를 테스트하려면 시스템의 문서 루트에 testsql.php라는 파일을 만듭니다. Ubuntu, Debian 및 Redhat에서는 `/var/www/html/`, SUSE에서는 `/srv/www/htdocs`, Alpine에서는 `/var/www/localhost/htdocs`, macOS에서는 `/usr/local/var/www`입니다. 다음 스크립트를 파일에 복사하고 서버, 데이터베이스, 사용자 이름 및 암호를 적절하게 바꿉니다.

```php
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

function exception_handler($exception) {
    echo "<h1>Failure</h1>";
    echo "Uncaught exception: " , $exception->getMessage();
    echo "<h1>PHP Info for troubleshooting</h1>";
    phpinfo();
}

set_exception_handler('exception_handler');

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Success Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "<h1>SQL Error:</h1>";
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```

브라우저에서 https://localhost/testsql.php (macOS에서는 https://localhost:8080/testsql.php )를 가리킵니다. SQL Server/Azure SQL 데이터베이스에 연결할 수 있어야 합니다. SQL 버전 정보를 보여 주는 성공 메시지가 표시되지 않으면 명령줄에서 스크립트를 실행하여 몇 가지 기본적인 문제 해결을 수행할 수 있습니다.

```bash
php testsql.php
```

명령줄에서 실행에 성공했지만 브라우저에 아무것도 표시되지 않으면 [Apache 로그 파일](https://linuxize.com/post/apache-log-files/#location-of-the-log-files)을 확인합니다. [지원 리소스](support-resources-for-the-php-sql-driver.md)에서 도움을 받을 수 있는 위치를 참조하세요.

## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)
