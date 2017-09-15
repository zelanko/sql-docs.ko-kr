---
title: "PHP SQL 드라이버 로드 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cb2200b2c5d151981e9dcdf8322dd7c43b91c6ee
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="loading-the-php-sql-driver"></a>PHP SQL 드라이버 로드
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 항목에서는 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 를 PHP 프로세스 공간에 로드하는 방법에 대한 지침을 제공합니다.  
  
드라이버 로드에는 두 가지 옵션이 있습니다. PHP를 시작하거나 PHP 스크립트 런타임에 드라이버를 로드할 수 있습니다.  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>확장 디렉터리로 드라이버 파일 이동  
사용하는 절차에 관계없이 첫 번째 단계에서는 PHP 런타임에서 찾을 수 있는 디렉터리에 드라이버 파일을 넣습니다. 그러므로 드라이버 파일을 PHP 확장 디렉터리에 넣습니다. [를 사용하여 설치되는 드라이버 파일의 목록을 보려면](../../connect/php/system-requirements-for-the-php-sql-driver.md) PHP SQL Driver 시스템 요구 사항 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]을 참조하세요.  
  
필요한 경우 드라이버 파일의 디렉터리 위치를 PHP 구성 파일 (php.ini)에 지정를 사용 하는 **extension_dir** 옵션입니다. 예를 들어 c:\php\ext 디렉터리에 드라이버 파일을 넣는 경우 다음 옵션을 사용하세요.  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>PHP를 시작할 때 드라이버 로드  
PHP를 시작할 때 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 를 로드하려면 먼저 드라이버 파일을 확장 디렉터리로 이동합니다. 그런 후 다음 단계를 수행합니다.  
  
1.  사용할 수 있도록는 **SQLSRV** 드라이버를 수정 **php.ini** 확장 섹션에 다음 줄을 추가 하거나 이미 목록에 있는 줄을 수정 하 여:  
  
    Windows (이 예에서는 PHP 7 버전 4.0 스레드 보안 드라이버를 사용 하는 데 사용): 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    Linux (이 예에서는 PECL으로 설치 된 버전을 사용 하는 데 사용): 
    ```  
    extension=sqlsrv.so  
    ```  
    사용할 수 있도록는 **PDO_SQLSRV** 드라이버를 수정 **php.ini** 확장 섹션에 다음 줄을 추가 하거나 이미 목록에 있는 줄을 수정 하 여:  
  
    Windows (이 예에서는 PHP 7 버전 4.0 스레드 보안 드라이버를 사용 하는 데 사용):
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    Linux (이 예에서는 PECL으로 설치 된 버전을 사용 하는 데 사용):
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  사용 하려는 경우는 **PDO_SQLSRV** 드라이버를 기본 제공 확장 이나 동적으로 로드 된 확장으로 PHP 데이터 개체 (PDO) 확장으로 사용할 수 있어야 합니다. PDO_SQLSRV 드라이버를 동적으로 로드 해야 하는 경우 php_pdo.dll (또는 Linux에서 pdo.so) 확장 디렉터리에 존재 해야 하 고 다음 줄이 php.ini에 있어야 하는 데 필요한 합니다.

    Windows:  
    ```
    extension=php_pdo.dll  
    ```  
    Linux:  
    ```
    extension=pdo.so  
    ```  
  
3.  웹 서버를 다시 시작합니다.  
  
> [!NOTE]  
> 드라이버가 성공적으로 로드 되었는지 여부를 확인 하려면 호출 하는 스크립트를 실행 [phpinfo ()](http://go.microsoft.com/fwlink/?LinkId=108678)합니다.  
  
**php.ini** 지시문에 대한 자세한 내용은 [핵심 php.ini 지시문 설명](http://go.microsoft.com/fwlink/?LinkId=105817)을 참조하세요.  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>PHP 스크립트 런타임 시 드라이버 로드  
스크립트 런타임 시 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 를 로드하려면 먼저 드라이버 파일을 확장 디렉터리로 이동합니다. 그런 다음 드라이버의 파일 이름과 일치 하는 PHP 스크립트의 시작 부분에 다음 줄을 포함 합니다.  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
동적 확장 로드와 관련 된 PHP 함수에 대 한 자세한 내용은 참조 [dl](http://go.microsoft.com/fwlink/?LinkId=105818) 및 [extension_loaded 합니다.](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>관련 항목:  
[시작](../../connect/php/getting-started-with-the-php-sql-driver.md)
[를 사용하여 설치되는 드라이버 파일의 목록을 보려면](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[프로그래밍 가이드](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
  

