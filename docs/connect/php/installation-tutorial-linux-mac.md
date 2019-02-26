---
title: Linux 및 macOS Microsoft Drivers for PHP for SQL Server에 대 한 설치 자습서 | Microsoft Docs
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: a31b17b8fbe2130b84b27be08d1a6218d697f9f2
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744633"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux 및 macOS Microsoft Drivers for PHP for SQL Server에 대 한 설치 자습서
다음 지침을 정리 된 환경을 가정 및 PHP 7.x, Microsoft ODBC driver, Apache, 및 Microsoft Drivers for PHP for SQL Server ubuntu 16.04, 18.04, 및 18.10, 7, RedHat Debian 8 및 9를 설치 하는 방법을 보여 줍니다 Suse 12 및 15 및 macOS 10.12 10.13, 및 10.14 합니다. 이러한 지침은 PECL를 사용 하 여 드라이버를 설치 하는 것이 좋습니다 하지만에서 미리 작성 된 이진 파일을 다운로드할 수도 있습니다는 [&#40;microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지 및 의지침에따라설치[ Loading the Microsoft Drivers for PHP for SQL Server](../../connect/php/loading-the-php-sql-driver.md)합니다. 에 대 한 확장 로드 및 php.ini에 확장을 추가할 것 수행 되는 이유는 설명은 섹션을 참조 [드라이버 로드](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup)합니다.

이러한 지침은 기본적으로 PHP 7.3를 설치합니다. 참고 일부 지원 되는 Linux 배포판 기본 PHP 7.0 또는 이전 버전에서는 SQL Server-용 PHP 드라이버에 대 한 지원 되지 않는 대신 PHP 7.1 또는 7.2를 설치 하려면 각 섹션의 시작 부분에 정보를 참조 하십시오.

## <a name="contents-of-this-page"></a>이 페이지의 내용:

- [Ubuntu 16.04, 18.04, 및 18.10 드라이버 설치](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Red Hat 7에 드라이버를 설치합니다.](#installing-the-drivers-on-red-hat-7)
- [Debian 8 및 9 드라이버 설치](#installing-the-drivers-on-debian-8-and-9)
- [Suse 12 및 15에 드라이버를 설치합니다.](#installing-the-drivers-on-suse-12-and-15)
- [MacOS Sierra, High Sierra 및 Mojave 드라이버 설치](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>Ubuntu 16.04, 18.04, 및 18.10 드라이버 설치

> [!NOTE]
> 설치 PHP 7.1 또는 7.2, 7.1 또는 7.2 다음 명령에서 사용 하 여 7.3을 대체 합니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
다음 지침에 따라 Ubuntu 용 ODBC 드라이버를 설치 합니다 [Linux 및 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버 설치
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache를 다시 시작 하 고 테스트 샘플 스크립트
```
sudo service apache2 restart
```
설치를 테스트 하려면를 참조 하세요 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-red-hat-7"></a>Red Hat 7에 드라이버를 설치합니다.

> [!NOTE]
> PHP 7.1 또는 7.2를 설치 하려면 다음 명령에서 각각 remi php72 remi php71와 remi php73를 대체 합니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
다음 지침에 따라 Red Hat 7에 대 한 ODBC 드라이버를 설치 합니다 [Linux 및 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

PECL PHP 7.2 또는 7.3을 사용 하 여 PHP 드라이버 컴파일 기본값 보다 더 최신 GCC를 필요 합니다.
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버 설치
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
PECL 문제 GCC로 업그레이드 하는 경우에 드라이버의 최신 버전의 올바른 설치를 하지 못할 수 있습니다. 설치, 패키지를 다운로드 및 컴파일할 수동으로 (pdo_sqlsrv에 대 한 유사한 단계):
```
pecl download sqlsrv
tar xvzf sqlsrv-5.6.0.tgz
cd sqlsrv-5.6.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
또는에서 미리 작성 된 이진 파일을 다운로드할 수 있습니다 합니다 [Github 프로젝트 페이지](https://github.com/Microsoft/msphpsql/releases), 또는 Remi 리포지토리에서 설치:
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>4단계. Apache 설치
```
sudo yum install httpd
```
SELinux는 기본적으로 설치 하 고 문서 모드에서 실행 됩니다. SELinux 통해 데이터베이스에 연결 하는 Apache를 허용 하려면 다음 명령을 실행 합니다.
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache를 다시 시작 하 고 테스트 샘플 스크립트
```
sudo apachectl restart
```
설치를 테스트 하려면를 참조 하세요 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Debian 8 및 9 드라이버 설치

> [!NOTE]
> PHP 7.1 또는 7.2를 설치 하려면 다음 명령에서 7.3을 7.1 또는 7.2 바꿉니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
다음 지침에 따라 Debian 용 ODBC 드라이버를 설치 합니다 [Linux 및 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다. 

브라우저에서 올바르게 표시 하려면 PHP 출력을 가져올 올바른 로캘로 생성 해야 합니다. 예를 들어 en_US u t F-8 로캘에 대 한 다음 명령을 실행 합니다.
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버 설치
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache를 다시 시작 하 고 테스트 샘플 스크립트
```
sudo service apache2 restart
```
설치를 테스트 하려면를 참조 하세요 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Suse 12 및 15에 드라이버를 설치합니다.

> [!NOTE]
> 다음 지침에서는 대체 <SuseVersion> Suse-의 버전을 사용 하 여 Suse Enterprise Linux 15를 사용 하는 경우 됩니다 SLE_15 또는 SLE_15_SP1, 및 다른 버전에 대 한 유사 합니다. -Suse Linux의 모든 버전을 참조 하세요 PHP의 일부 버전을 사용할 수 `http://download.opensuse.org/repositories/devel:/languages:/php` Suse 버전 버전이 기본 PHP를 사용할 수를 확인 하려면 또는 `http://download.opensuse.org/repositories/devel:/languages:/php:/` 다른 버전의 PHP는를 참조 하는 Suse 버전에 사용할 수 있습니다.

> [!NOTE]
> PHP 7.3 패키지 Suse 12에 대 한 제공 되지 않습니다. 다음 URL로 PHP 7.1을 설치 하려면 아래 리포지토리 URL을 바꿉니다: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`합니다.
> 다음 URL로 PHP 7.2를 설치 하려면 아래 리포지토리 URL을 바꿉니다: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`합니다.

### <a name="step-1-install-php"></a>1단계. PHP 설치
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
다음 지침에 따라 Suse에 대 한 ODBC 드라이버를 설치 합니다 [Linux 및 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버 설치
> [!NOTE]
> 오류 메시지가 표시 되 면 `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`에서 /usr/bin/pecl pecl 스크립트 편집 및 제거는 `-n` 마지막 줄에서 전환 합니다. 이 스위치는 OpenSSL 확장 로드 못하게 하는 PHP를 호출할 때 ini 파일을 로드할 PECL을 방지 합니다.

```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache를 다시 시작 하 고 테스트 샘플 스크립트
```
sudo systemctl restart apache2
```
설치를 테스트 하려면를 참조 하세요 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>MacOS Sierra, High Sierra 및 Mojave 드라이버 설치

수 없는 것을 하는 경우 아래와 같이 brew를 설치 합니다.
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> PHP 7.1 또는 7.2를 설치 하려면 교체 php@7.3 사용 하 여 php@7.1 또는 php@7.2 다음 명령에서 각각.

### <a name="step-1-install-php"></a>1단계. PHP 설치

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP 실행 경로-이제 수 `php -v` 에 올바른 버전의 PHP가 실행 중인지 확인 합니다. PHP가 경로에 올바른 버전이 아닌, 하는 경우 다음을 실행 합니다.
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>2단계. 필수 구성 요소 설치
다음 지침에 따라 macOS에 대 한 ODBC 드라이버를 설치 합니다 [Linux 및 macOS 설치 페이지](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)합니다. 

또한 GNU 확인 도구를 설치 해야 할 수 있습니다.
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>3단계. Microsoft SQL Server 용 PHP 드라이버 설치
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>4단계. Apache를 설치 하 고 드라이버 로드를 구성 합니다.
```
brew install apache2
```
Apache Apache 설치에 대 한 구성 파일을 찾으려면 실행 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
에 대 한 경로 대체 하 고 `httpd.conf` 다음 명령에서:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>5단계. Apache를 다시 시작 하 고 테스트 샘플 스크립트
```
sudo apachectl restart
```
설치를 테스트 하려면를 참조 하세요 [설치 테스트에](#testing-your-installation) 이 문서의 끝입니다.

## <a name="testing-your-installation"></a>설치 테스트

이 샘플 스크립트를 테스트 하려면 시스템의 문서 루트에서 testsql.php 이라는 파일을 만듭니다. 이것이 `/var/www/html/` Redhat, Ubuntu, Debian에 `/srv/www/htdocs` SUSE에 또는 `/usr/local/var/www` macOS에서. 서버, 데이터베이스, 사용자 이름 및 암호를 적절 한 대체를 다음 스크립트를 복사 합니다.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

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

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
브라우저를 가리키면 https://localhost/testsql.php (https://localhost:8080/testsql.php macOS에서). 이제 SQL Server/Azure SQL database에 연결할 수 있어야 합니다.

## <a name="see-also"></a>참고 항목  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 로드](../../connect/php/loading-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)
