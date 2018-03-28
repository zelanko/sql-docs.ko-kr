---
title: SQL Server 용 Microsoft Drivers for PHP 로드 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5a21dcd1f7f416a7bdade75e1648aec9795680a1
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server 로드
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

로드에 대 한 지침을 제공 하는이 페이지는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 를 PHP 프로세스 공간입니다.  
  
사용 중인 플랫폼에 대 한 미리 작성 된 드라이버를 다운로드할 수 있습니다는 [Microsoft Drivers for PHP for SQL Server](https://github.com/Microsoft/msphpsql/releases) Github 프로젝트 페이지. 각 설치 패키지는 스레드 및 스레드 비 variants에 SQLSRV 및 PDO_SQLSRV 드라이버 파일을 포함 합니다. windows에서 32 비트 및 64 비트 변형에서 사용할 수 있습니다. 참조 [Microsoft Drivers for PHP for SQL Server에 대 한 시스템 요구 사항](../../connect/php/system-requirements-for-the-php-sql-driver.md) 각 패키지에 포함 된 드라이버 파일의 목록에 대 한 합니다. 드라이버 파일은 PHP 버전, 아키텍처 및 PHP 환경의 threadedness 일치 해야 합니다.

Linux와 macOS에서 드라이버 수 또는 설치에서 볼 수 있는 PECL를 사용 하 여 [설치 자습서](../../connect/php/installation-tutorial-linux-mac.md)합니다.
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>확장 디렉터리로 드라이버 파일 이동  
PHP 런타임에서 찾을 수 있는 디렉터리에 드라이버 파일이 있어야 합니다. 기본 디렉터리를 찾을, 실행을 기본 PHP 확장 디렉터리-에 드라이버 파일을 저장 하는 것이 더 편리 `php -i | sls extension_dir` windows 또는 `php -i | grep extension_dir` Linux/macOS에서. 기본 확장 디렉터리를 사용 하지 않는 경우 PHP 구성 파일 (php.ini)에 디렉터리를 지정를 사용 하 여 **extension_dir** 옵션입니다. 드라이버 파일 저장 하는 경우에 예를 들어 프로그램 `c:\php\ext` 디렉터리 php.ini에 다음 줄 추가:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>PHP를 시작할 때 드라이버 로드  
SQLSRV 드라이버를 PHP를 시작할 때 로드 하려면 먼저 드라이버 파일을 확장 디렉터리로 이동 합니다. 그런 후 다음 단계를 수행합니다.  
  
1.  사용할 수 있도록는 **SQLSRV** 드라이버를 수정 **php.ini** 확장 섹션에 다음 줄을 추가 하 여 적절 하 게 파일 이름 변경:  
  
    Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    Linux 배포판에 대 한 미리 작성 된 이진 파일을 다운로드 한 경우: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    SQLSRV 이진 PECL 또는 소스에서 컴파일한 경우 대신이 연결의 이름은 sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  사용할 수 있도록는 **PDO_SQLSRV** 드라이버를 기본 제공 확장 이나 동적으로 로드 된 확장으로 PHP 데이터 개체 (PDO) 확장으로 사용할 수 있어야 합니다.

    Windows에서는 미리 작성 된 PHP 이진 파일은 기본 제공, PDO 때문 php.ini 로드 하는 것을 수정할 필요가 없습니다. 그러나 PHP 소스에서 컴파일된을 한 빌드할 수에 대 한 별도 PDO 확장을 지정 하는 경우 연결의 이름은 `php_pdo.dll`, 확장 디렉터리에 복사 및 php.ini에 다음 줄을 추가 해야 합니다.  
    ```
    extension=php_pdo.dll  
    ```
    Linux 시스템의 패키지 관리자를 사용 하 여 PHP를 설치한 경우 PDO가 아마도 설치 pdo.so 라는 동적으로 로드 된 확장으로 합니다. PDO_SQLSRV 확장 하기 전에 PDO 확장을 로드 해야 합니다 또는 로드에 실패 합니다. 확장은 주로 개별.ini 파일을 사용 하 여 로드 하 고 php.ini 후 이러한 파일을 읽습니다. 따라서 pdo.so 자체.ini 파일을 통해 로드 되 면 PDO 후 PDO_SQLSRV 드라이버를 로드 하는 별도 파일은 필요 합니다. 

    디렉터리 확장 프로그램별.ini 파일을 가리키는 확인 하려면 실행 `php --ini` 아래에 디렉터리를 입력 하 고 `Scan for additional .ini files in:`합니다. Pdo.so를 로드 하는 파일을 찾을-에 숫자를 10 pdo.ini 기수가 가능성이 높습니다. 숫자 접두사 숫자 접두사를 갖지 않는 파일은 사전순으로 로드 하는 동안.ini 파일의 로드 순서를 나타냅니다. 30-pdo_sqlsrv.ini (pdo.ini works 접두사를 추가 하는 보다 큰 숫자) 또는 pdo_sqlsrv.ini (pdo.ini 번호로 접두사가 붙지은) 하는 경우, 호출 PDO_SQLSRV 드라이버 파일을 로드 하 고 파일 이름으로 변경, 다음 줄을 추가 하려면 파일 만들기 적절 한:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    으로 SQLSRV와 PDO_SQLSRV 이진 PECL, 또는 원본에서 컴파일한 경우 대신이 연결의 이름은 pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    이 파일을 다른.ini 파일이 포함 된 디렉터리로 복사 합니다. 

    PDO 지원이 기본 제공 되는 소스에서 PHP를 컴파일한 경우 별도.ini 파일이 필요 하지 않은 및 php.ini에 위의 적절 한 줄을 추가할 수 있습니다.
  
3.  웹 서버를 다시 시작합니다.  
  
> [!NOTE]  
> 드라이버가 성공적으로 로드 되었는지 여부를 확인 하려면 호출 하는 스크립트를 실행 [phpinfo ()](http://php.net/manual/en/function.phpinfo.php)합니다.  
  
에 대 한 자세한 내용은 **php.ini** 지시문 참조 [핵심 php.ini 지시문 설명](http://php.net/manual/en/ini.core.php)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[시작 Microsoft Drivers for PHP for SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[시스템 요구 사항을 Microsoft Drivers for PHP for SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[SQL Server 용 PHP 용 Microsoft 드라이버에 대 한 가이드를 프로그래밍](../../connect/php/programming-guide-for-php-sql-driver.md)

[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV 드라이버 API 참조](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
