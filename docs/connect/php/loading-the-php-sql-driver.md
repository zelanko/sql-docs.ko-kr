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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67936389"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 로드
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 PHP 프로세스 공간에 로드하는 방법에 대한 지침을 제공합니다.  
  
[Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지에서 플랫폼에 대한 미리 빌드된 드라이버를 다운로드할 수 있습니다. 각 설치 패키지에는 스레드 및 비스레드 변형의 SQLSRV 및 PDO_SQLSRV 드라이버 파일이 포함되어 있습니다. Windows에서는 32비트 및 64비트 변형도 사용할 수 있습니다. 각 패키지에 포함된 드라이버 파일 목록을 보려면 [Microsoft Drivers for PHP for SQL Server 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)을 참조하세요. 드라이버 파일은 PHP 환경의 PHP 버전, 아키텍처 및 스레드 여부가 일치해야 합니다.

Linux 및 macOS에서는 [설치 자습서](../../connect/php/installation-tutorial-linux-mac.md)에서 설명한 대로 PECL를 사용하여 드라이버를 설치할 수 있습니다.

PHP를 빌드하거나 `phpize`를 사용하여 원본에서 드라이버를 빌드할 수도 있습니다. 원본에서 드라이버를 빌드하도록 선택하는 경우 PHP를 빌드할 때 `--enable-sqlsrv=static --with-pdo_sqlsrv=static`(Linux 및 macOS) 또는 `--enable-sqlsrv=static --with-pdo-sqlsrv=static`(Windows)를 `./configure` 명령에 추가하여 공유 확장으로 빌드하는 대신 PHP에 정적으로 빌드할 수 있습니다. PHP 빌드 시스템 및 `phpize`에 대한 자세한 내용은 [PHP 설명서](http://php.net/manual/install.php)를 참조하세요.
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>확장 디렉터리로 드라이버 파일 이동  
드라이버 파일은 PHP 런타임이 찾을 수 있는 디렉터리에 있어야 합니다. 기본 PHP 확장 디렉터리에 드라이버 파일을 배치하는 것이 가장 쉽습니다. 기본 디렉터리를 찾으려면 Windows의 경우 `php -i | sls extension_dir` 또는 Linux/macOS의 경우 `php -i | grep extension_dir`를 실행합니다. 기본 확장명 디렉터리를 사용하지 않는 경우 **extension_dir** 옵션을 사용하여 PHP 구성 파일(php.ini)에서 디렉터리를 지정합니다. 예를 들어 Windows의 경우 `c:\php\ext` 디렉터리에 드라이버 파일을 추가한 경우 다음 줄을 php.ini에 추가합니다.
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>PHP를 시작할 때 드라이버 로드  
PHP를 시작할 때 SQLSRV 드라이버를 로드하려면 먼저 드라이버 파일을 확장 디렉터리로 이동합니다. 그런 후 다음 단계를 수행합니다.  
  
1.  **SQLSRV** 드라이버를 사용하도록 설정하려면 확장 섹션에 다음 줄을 추가하고 파일 이름을 적절하게 변경하여 **php.ini**를 수정합니다.  
  
    Windows에서: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Linux에서 배포를 위해 미리 빌드된 이진 파일을 다운로드한 경우: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    원본에서 또는 PECL를 사용하여 SQLSRV 이진 파일을 컴파일하면 이름이 sqlsrv.so로 지정됩니다.
    ```
    extension=sqlsrv.so
    ```
  
2.  **PDO_SQLSRV** 드라이버를 사용하려는 경우 PDO(PHP Data Objects)를 기본 제공 확장이나 동적으로 로드된 확장으로 사용할 수 있어야 합니다.

    Windows에서는 미리 빌드된 PHP 이진 파일에 PDO를 기본 제공하므로 이를 로드하기 위해 php.ini를 수정할 필요가 없습니다. 그러나 PHP를 원본에서 컴파일하고 빌드할 개별 PDO 확장을 지정한 경우 이름이 `php_pdo.dll`로 지정되므로 이를 확장 디렉터리에 복사하고 다음 줄을 PHP에 추가해야 합니다.  
    ```
    extension=php_pdo.dll  
    ```
    Linux에서 시스템의 패키지 관리자를 사용하여 PHP를 설치한 경우 PDO는 pdo.so라는 동적으로 로드된 확장으로 설치될 수 있습니다. PDO_SQLSRV 확장 전에 PDO 확장을 로드해야 합니다. 그렇지 않으면 로드에 실패합니다. 확장은 일반적으로 개별 .ini 파일을 사용하여 로드되고 이러한 파일은 php.ini 다음에 읽힙니다. 따라서 pdo.so가 자체 .ini 파일을 통해 로드된 경우 PDO 다음에 PDO_SQLSRV 드라이버를 로드하는 별도의 파일이 필요합니다. 

    확장 관련 .ini 파일이 있는 디렉터리를 확인하려면 `php --ini`를 실행하고 `Scan for additional .ini files in:`에 나열된 디렉터리를 확인합니다. pdo.so를 로드하는 파일을 찾습니다 .이 파일에는 숫자가 접두사로 추가될 수 있습니다(예: 10-pdo). 숫자 접두사는 .ini 파일의 로드 순서를 나타내지만 숫자 접두사가 없는 파일은 사전순으로 로드됩니다. 30-pdo_sqlsrv.ini(pdo.ini에 지정된 접두사보다 큰 임의의 숫자) 또는 pdo_sqlsrv.ini(pdo.ini에 숫자 접두사가 지정되지 않은 경우)라는 파일을 만들어 PDO_SQLSRV 드라이버 파일을 로드하고, 여기에 다음 줄을 추가하여 파일 이름을 적절하게 변경합니다.  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    SQLSRV와 마찬가지로 원본에서 또는 PECL을 사용하여 PDO_SQLSRV 이진 파일을 컴파일하면 이름이 pdo_sqlsrv로 지정됩니다.
    ```
    extension=pdo_sqlsrv.so
    ```
    이 파일을 다른 .ini 파일이 포함된 디렉터리로 복사합니다. 

    기본 제공 PDO 지원을 사용하여 원본에서 PHP를 컴파일한 경우 별도의 .ini 파일이 필요하지 않으며, 위의 적절한 줄을 php.ini에 추가할 수 있습니다.
  
3.  웹 서버를 다시 시작합니다.  
  
> [!NOTE]  
> 드라이버가 성공적으로 로드되었는지 여부를 확인하려면 [phpinfo()](https://php.net/manual/en/function.phpinfo.php)를 호출하는 스크립트를 실행합니다.  
  
**php.ini** 지시문에 대한 자세한 내용은 [핵심 php.ini 지시문 설명](https://php.net/manual/en/ini.core.php)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[Microsoft Drivers for PHP for SQL Server 시작](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server 프로그래밍 가이드 | Microsoft Docs](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
