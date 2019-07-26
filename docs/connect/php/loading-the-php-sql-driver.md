---
title: Microsoft Drivers for PHP for SQL Server 로드 | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936389"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 로드
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 PHP 프로세스 공간에 로드하는 방법에 대한 지침을 제공합니다.  
  
Microsoft driver for [PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지에서 플랫폼에 대 한 미리 빌드된 드라이버를 다운로드할 수 있습니다. 각 설치 패키지에는 스레드 및 비 스레드 변형의 SQLSRV 및 PDO_SQLSRV 드라이버 파일이 포함 되어 있습니다. Windows에서는 32 비트 및 64 비트 변형 에서도 사용할 수 있습니다. 각 패키지에 포함 된 드라이버 파일 목록에 대 한 자세한 내용은 Microsoft driver for [SQL SERVER PHP에 대 한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md) 을 참조 하세요. 드라이버 파일은 php 환경의 PHP 버전, 아키텍처 및 threadedness 일치 해야 합니다.

Linux 및 macOS에서 [설치 자습서](../../connect/php/installation-tutorial-linux-mac.md)에 나와 있는 것 처럼 PECL를 사용 하 여 드라이버를 설치할 수도 있습니다.

PHP를 빌드하거나를 사용 `phpize`하 여 원본에서 드라이버를 빌드할 수도 있습니다. 원본에서 드라이버를 작성 하도록 선택 하는 경우 (Linux 및 macos) 또는 `--enable-sqlsrv=static --with-pdo_sqlsrv=static` `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (Windows)를 `./configure` 명령에 추가 하 여 공유 확장으로 빌드하는 대신 PHP에 정적으로 빌드할 수 있습니다. PHP를 빌드하고 있습니다. Php 빌드 시스템 및 `phpize`에 대 한 자세한 내용은 [php 설명서](http://php.net/manual/install.php)를 참조 하세요.
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>확장 디렉터리로 드라이버 파일 이동  
드라이버 파일은 PHP 런타임에서 찾을 수 있는 디렉터리에 있어야 합니다. 기본 PHP 확장 디렉터리에 드라이버 파일을 배치 하는 것이 가장 쉽습니다. 기본 디렉터리를 찾으려면 Windows 또는 `php -i | sls extension_dir` `php -i | grep extension_dir` Linux/macos에서 실행 합니다. 기본 확장명 디렉터리를 사용 하지 않는 경우 **extension_dir** 옵션을 사용 하 여 php 구성 파일 (php)에서 디렉터리를 지정 합니다. 예를 들어 Windows에서 `c:\php\ext` 디렉터리에 드라이버 파일을 추가한 경우 다음 줄을 php에 추가 합니다.
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>PHP를 시작할 때 드라이버 로드  
PHP를 시작할 때 SQLSRV 드라이버를 로드하려면 먼저 드라이버 파일을 확장 디렉터리로 이동합니다. 그런 후 다음 단계를 수행합니다.  
  
1.  **SQLSRV** 드라이버를 사용 하도록 설정 하려면 확장 섹션에 다음 줄을 추가 하 여 **php** 를 수정 하 고 파일 이름을 적절 하 게 변경 합니다.  
  
    Windows의 경우: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Linux에서 배포를 위해 미리 빌드된 이진 파일을 다운로드 한 경우: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    원본 또는 PECL를 사용 하 여 SQLSRV binary를 컴파일하면 이름이 sqlsrv.so로 지정 됩니다.
    ```
    extension=sqlsrv.so
    ```
  
2.  **PDO_SQLSRV** 드라이버를 사용 하도록 설정 하려면 PDO (PHP Data Objects) 확장을 기본 제공 확장 또는 동적으로 로드 된 확장으로 사용할 수 있어야 합니다.

    Windows에서는 미리 빌드된 PHP 이진 파일에 PDO를 기본으로 제공 하므로이를 로드 하기 위해 php를 수정할 필요가 없습니다. 그러나 소스에서 PHP를 컴파일 했 고 빌드할 개별 PDO 확장을 지정 하는 경우 이름이 `php_pdo.dll`로 지정 되며,이를 확장 디렉터리에 복사 하 고 다음 줄을 PHP에 추가 해야 합니다.  
    ```
    extension=php_pdo.dll  
    ```
    Linux에서 시스템의 패키지 관리자를 사용 하 여 PHP를 설치한 경우 PDO는 pdo.so 이라는 동적으로 로드 된 확장으로 설치 될 수 있습니다. PDO_SQLSRV 확장 전에 PDO 확장을 로드 해야 합니다. 그렇지 않으면 로드에 실패 합니다. 확장명은 일반적으로 개별 .ini 파일을 사용 하 여 로드 되 고 이러한 파일은 php를 사용 하 여 읽습니다. 따라서 pdo.so 파일을 통해 로드 된 경우 PDO를 만든 후 PDO_SQLSRV 드라이버를 로드 하는 별도의 파일이 필요 합니다. 

    확장 특정 .ini 파일이 있는 디렉터리를 확인 하려면를 실행 `php --ini` 하 고 아래 `Scan for additional .ini files in:`에 나열 된 디렉터리를 확인 합니다. Pdo.so를 로드 하는 파일을 찾습니다 .이 파일에는 숫자 (예: 10-pdo)가 접두사로 추가 될 수 있습니다. 숫자 접두사는 .ini 파일의 로드 순서를 나타내지만 숫자 접두사가 없는 파일은 사전순으로 로드 됩니다. PDO_SQLSRV 드라이버 파일을 로드 하는 파일을 만들고 30-pdo_sqlsrv (pdo를 접두사로 사용한 것 보다 큰 숫자) 또는 PDO_SQLSRV (pdo에 숫자가 접두사로 표시 되지 않는 경우)를 로드 하 고 다음 줄을 추가 하 여 파일 이름을로 변경 합니다. 적당  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    SQLSRV와 마찬가지로 source에서 PDO_SQLSRV binary를 컴파일하거나 PECL를 사용 하 여 컴파일한 경우에는 대신 PDO_SQLSRV로 이름이 지정 됩니다.
    ```
    extension=pdo_sqlsrv.so
    ```
    이 파일을 다른 .ini 파일이 포함 된 디렉터리로 복사 합니다. 

    기본 제공 PDO 지원을 사용 하 여 원본에서 PHP를 컴파일한 경우 별도의 .ini 파일이 필요 하지 않으며, 위의 적절 한 줄을 PHP .ini에 추가할 수 있습니다.
  
3.  웹 서버를 다시 시작합니다.  
  
> [!NOTE]  
> 드라이버가 성공적으로 로드되었는지 여부를 확인하려면 [phpinfo()](https://php.net/manual/en/function.phpinfo.php)를 호출하는 스크립트를 실행합니다.  
  
**php.ini** 지시문에 대한 자세한 내용은 [핵심 php.ini 지시문 설명](https://php.net/manual/en/ini.core.php)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
