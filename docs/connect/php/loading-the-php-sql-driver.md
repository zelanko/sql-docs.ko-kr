---
title: Microsoft Drivers for PHP for SQL Server 로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
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
manager: craigg
ms.openlocfilehash: 3dd99ffa39de48dbf8839cbe06a8bb236fffbdf3
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606203"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 로드
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]를 PHP 프로세스 공간에 로드하는 방법에 대한 지침을 제공합니다.  
  
사용 중인 플랫폼에 대 한 미리 작성 된 드라이버를 다운로드할 수 있습니다 합니다 [&#40;microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지. 각 설치 패키지는 스레드 및 스레드 비 variant의 SQLSRV 및 PDO_SQLSRV 드라이버 파일을 포함합니다. Windows에서 32 비트 및 64 비트 변형에서 사용할 수 있습니다. 참조 [Microsoft Drivers for PHP for SQL Server에 대 한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md) 각 패키지에 포함 된 드라이버 파일의 목록에 대 한 합니다. 드라이버 파일에는 PHP 버전, 아키텍처 및 PHP 환경의 threadedness 일치 해야 합니다.

Linux 및 macOS에서 드라이버 또는 설치할 수 있는 PECL를 사용 하 여 [설치 자습서](../../connect/php/installation-tutorial-linux-mac.md)합니다.
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>확장 디렉터리로 드라이버 파일 이동  
PHP 런타임을 찾을 수 있는 디렉터리에 드라이버 파일이 있어야 합니다. 기본 PHP 확장 디렉터리-실행 하는 기본 디렉터리 찾기에 드라이버 파일을 저장 하는 것이 쉽습니다 `php -i | sls extension_dir` Windows에서 또는 `php -i | grep extension_dir` Linux/macOS에서. 기본 확장 디렉터리를 사용 하지 않는 경우 PHP 구성 파일 (php.ini)에서 디렉터리를 지정를 사용 하 여 **extension_dir** 옵션입니다. 예를 들어, Windows, 드라이버 파일에 저장 하는 경우에 프로그램 `c:\php\ext` 디렉터리 php.ini에 다음 줄을 추가 합니다.
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>PHP를 시작할 때 드라이버 로드  
PHP를 시작할 때 SQLSRV 드라이버를 로드하려면 먼저 드라이버 파일을 확장 디렉터리로 이동합니다. 그런 후 다음 단계를 수행합니다.  
  
1.  사용 하도록 설정 합니다 **SQLSRV** 드라이버를 수정 **php.ini** 확장 섹션에 다음 줄을 더하여 파일 이름을 적절 하 게 변경:  
  
    Windows의 경우: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Linux에서 배포에 대 한 미리 작성 된 이진 파일을 다운로드 한 경우: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    SQLSRV 이진 PECL 또는 원본의 컴파일한 경우 대신 이름은 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  사용 하도록 설정 합니다 **PDO_SQLSRV** 드라이버를 기본 제공 확장으로 또는 동적으로 로드 된 확장으로 PHP 데이터 개체 (PDO) 확장을 사용할 수 있어야 합니다.

    Windows에서 미리 작성 된 PHP 이진 파일은 PDO 기본 제공 때문 php.ini 로드 하는 것을 수정 하지 않아도 됩니다. 그러나 이름은 PHP 소스에서 컴파일된을 한 별도 PDO 확장 프로그램을 빌드할 수를 지정 하는 경우 `php_pdo.dll`, 확장 디렉터리에 복사 하 고 php.ini에 다음 줄을 추가 해야 합니다.  
    ```
    extension=php_pdo.dll  
    ```
    Linux에서 시스템의 패키지 관리자를 사용 하 여 PHP를 설치 하는 경우 PDO 아마도 되어 pdo.so 라는 동적으로 로드 된 확장으로 합니다. PDO extension PDO_SQLSRV 확장 하기 전에 로드 해야 하거나 로드 하지 못합니다. 확장은 일반적으로 로드 하 여 개별.ini 파일을 사용 하 고 php.ini 후 이러한 파일을 읽습니다. 따라서 pdo.so 자체.ini 파일을 통해 로드 되 면 PDO 후 PDO_SQLSRV 드라이버를 로드 하는 별도 파일은 필요 합니다. 

    디렉터리 확장 프로그램별.ini 파일은 위치를 확인 하려면 `php --ini` 아래에 나열 된 디렉터리를 입력 하 고 `Scan for additional .ini files in:`입니다. Pdo.so를 로드 하는 파일을 찾을 가능성이 앞에 숫자를 10-pdo.ini-합니다. 숫자 접두사가 없는 파일은 사전순으로 로드 하는 동안 숫자 접두사는.ini 파일의 로드 순서를 나타냅니다. 30-pdo_sqlsrv.ini (접두사 pdo.ini 작동 하는 것 보다 큰 숫자) 또는 pdo_sqlsrv.ini (pdo.ini은 숫자로 시작 하지 않는) 하는 경우, 호출 PDO_SQLSRV 드라이버 파일을 로드할 파일 이름으로 변경 후에 다음 줄을 추가 하는 파일 만들기 적절 한:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    으로 SQLSRV를 사용 하 여 PDO_SQLSRV 이진 원본에서 또는 PECL를 사용 하 여 컴파일한 경우 대신 이름은 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    다른.ini 파일이 포함 된 디렉터리에이 파일을 복사 합니다. 

    PDO 지원이 기본 제공 되는 원본에서 PHP를 컴파일한 경우 수행할 필요가 없는 별도.ini 파일 및 php.ini에 위의 적절 한 줄을 추가할 수 있습니다.
  
3.  웹 서버를 다시 시작합니다.  
  
> [!NOTE]  
> 드라이버가 성공적으로 로드되었는지 여부를 확인하려면 [phpinfo()](https://php.net/manual/en/function.phpinfo.php)를 호출하는 스크립트를 실행합니다.  
  
**php.ini** 지시문에 대한 자세한 내용은 [핵심 php.ini 지시문 설명](https://php.net/manual/en/ini.core.php)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Microsoft Drivers for PHP for SQL Server에 대한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
