---
title: Linux와 macOS Microsoft Drivers for PHP for SQL Server에 대 한 설치 자습서 | Microsoft Docs
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: article
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.workload: Inactive
ms.openlocfilehash: f7c9542294be520b6861262e814b9fda31b06d5d
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux와 macOS Microsoft Drivers for PHP for SQL Server에 대 한 자습서 설치
다음 지침에서는 깨끗 한 환경 가정 및 Ubuntu 16.04 및 17.10, RedHat 7에서 SQL Server, Debian 8-9, Suse 12와 macOS X 10.11 및 10.12 PHP 용 PHP 7.x, Microsoft ODBC driver, Apache 및 Microsoft 드라이버를 설치 하는 방법을 보여 줍니다. 이러한 지침은 advise PECL를 사용 하 여 드라이버를 설치 하지만 미리 작성 된 이진 파일을 다운로드할 수도 있습니다는 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 페이지 프로젝트 및 지침 에설치[ SQL Server 용 Microsoft Drivers for PHP 로드](../../connect/php/loading-the-php-sql-driver.md)합니다. 섹션을 참조에 대 한 확장 로드 하 고 이유 म에 추가 하지 않는 확장 php.ini 설명은 [드라이버 로드](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)합니다.

-기본적으로 이러한 명령을 설치 PHP 7.2 PHP 7.0을 설치 하려면 각 섹션 이나 7.1의 시작 부분에 메모를 참조 하세요.

## <a name="contents-of-this-page"></a>이 페이지의 내용:

- [Ubuntu 16.04 및 17.10에 드라이버 설치](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [Red Hat 7에 드라이버 설치](#installing-the-drivers-on-red-hat-7)
- [Debian 8 및 9에 드라이버 설치](#installing-the-drivers-on-debian-8-and-9)
- [Suse 12에 드라이버 설치](#installing-the-drivers-on-suse-12)
- [El Capitan 및 시에라 macOS에 드라이버 설치](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>Ubuntu 16.04 및 17.10에 드라이버 설치

    > [!NOTE]
    > To install PHP 7.0 or 7.1, replace 7.2 with 7.0 or 7.1 in the following commands.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
지침에 따라 Ubuntu 용 ODBC 드라이버를 설치는 [Linux와 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버를 설치 합니다.
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 하 고 샘플 스크립트를 테스트 합니다.
```
sudo service apache2 restart
```
설치를 테스트 하려면 참조 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-red-hat-7"></a>Red Hat 7에 드라이버 설치

    > [!NOTE]
    > To install PHP 7.0 or 7.1, replace remi-php72 with remi-php70 or remi-php71 respectively in the following commands.

### <a name="step-1-install-php"></a>1단계. PHP 설치

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
지침에 따라 Red Hat 7에 대 한 ODBC 드라이버를 설치는 [Linux와 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

PHP 드라이버를 PHP 7.2 PECL 기본값 보다 더 최신 GCC 필요:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버를 설치 합니다.
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
PECL에서 문제 GCC를 업그레이드 한 경우에 최신 버전의 드라이버의 올바른 설치가 되지 않을 수 있습니다. 를 설치 하려면 패키지를 다운로드 하 고 수동으로 컴파일하십시오.
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
또는에서 미리 작성 된 이진 파일을 다운로드할 수 있습니다는 [Github 프로젝트 페이지](https://github.com/Microsoft/msphpsql/releases), 하거나 Remi 리포지토리에서 설치:
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>4단계. Apache 설치
```
sudo yum install httpd
```
SELinux는 기본적으로 설치 하 고 문서 모드에서 실행 됩니다. Apache SELinux 통해 데이터베이스 연결을 허용 하려면 다음 명령을 실행 합니다.
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 하 고 샘플 스크립트를 테스트 합니다.
```
sudo apachectl restart
```
설치를 테스트 하려면 참조 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Debian 8 및 9에 드라이버 설치

    > [!NOTE]
    > To install PHP 7.0 or 7.1, replace 7.2 in the following commands with 7.0 or 7.1.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
지침에 따라 Debian에 대 한 ODBC 드라이버를 설치는 [Linux와 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다. 

올바른 로캘로 브라우저에 올바르게 표시 하려면 PHP 출력을 생성 하려면 할 수도 있습니다. 예를 들어 en_US u t F-8 로캘에 대 한 다음 명령을 실행 합니다.
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버를 설치 합니다.
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 하 고 샘플 스크립트를 테스트 합니다.
```
sudo service apache2 restart
```
설치를 테스트 하려면 참조 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-suse-12"></a>Suse 12에 드라이버 설치

    > [!NOTE]
    > To install PHP 7.0, skip the command below adding the repository - 7.0 is the default PHP on suse 12.
    > To install PHP 7.1, replace the repository URL below with the following URL:
      `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
지침에 따라 Suse 12에 대 한 ODBC 드라이버를 설치는 [Linux와 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버를 설치 합니다.
```
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 하 고 샘플 스크립트를 테스트 합니다.
```
sudo systemctl restart apache2
```
설치를 테스트 하려면 참조 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>El Capitan 및 시에라 macOS에 드라이버 설치

이미 않아도 것, brew를 다음과 같이 설치:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

    > [!NOTE]
    > To install PHP 7.0 or 7.1, replace php72 with php70 or php71 respectively in the following commands.

### <a name="step-1-install-php"></a>1단계. PHP 설치

```
brew tap
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
brew install php72 --with-pear --with-httpd24 --with-cgi
echo 'export PATH="/usr/local/sbin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
지침에 따라 macOS에 대 한 ODBC 드라이버를 설치는 [Linux와 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다. 

또한 GNU 확인 도구를 설치 해야 할 수 있습니다.
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버를 설치 합니다.
```
chmod -R ug+w /usr/local/opt/php72/lib/php
pear config-set php_ini /usr/local/etc/php/7.2/php.ini system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache 다시 시작 하 고 샘플 스크립트를 테스트 합니다.
```
sudo apachectl restart
```
설치를 테스트 하려면 참조 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="testing-your-installation"></a>설치 테스트

이 샘플 스크립트를 테스트 하려면 시스템의 문서 루트에서 testsql.php 라는 파일을 만듭니다. 이 `/var/www/html/` Debian, Ubuntu와 Redhat, `/srv/www/htdocs` SUSE에 또는 `/usr/local/var/www` macOS에서 합니다. 서버, 데이터베이스, 사용자 이름 및 암호를 적절 하 게 교체, 다음 스크립트를 복사 합니다.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
브라우저를 http://localhost/testsql.php (http://localhost:8080/testsql.php macOS에서). 이제 SQL Server/Azure SQL 데이터베이스에 연결할 수 있습니다.

## <a name="see-also"></a>관련 항목:  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[SQL Server 용 Microsoft Drivers for PHP 로드](../../connect/php/loading-the-php-sql-driver.md)

[시스템 요구 사항을 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
