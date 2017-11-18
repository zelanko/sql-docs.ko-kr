---
title: "설명서의 코드 예제에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d24d29aba9db9d3626a456f87f799e00da1b42cc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="about-code-examples-in-the-documentation"></a>설명서의 코드 예제 정보
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 설명서의 코드 예제를 실행할 때 몇 가지 유의 사항이 있습니다.  
  
-   거의 모든 예제에서 SQL Server 2005 이상(버전 3.1을 사용하는 경우 SQL Server 2008 이상) 및 AdventureWorks 데이터베이스가 로컬 컴퓨터에 설치되어 있다고 가정합니다.  
  
    SQL Server 무료 버전 및 평가판 버전을 다운로드하는 방법에 대한 자세한 내용은 [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193)를 참조하세요.  
  
    AdventureWorks 데이터베이스를 다운로드하는 방법에 대한 자세한 내용은 [Microsoft SQL Server 샘플 및 커뮤니티 프로젝트](http://go.microsoft.com/fwlink/?LinkID=67739)를 참조하세요.  
  
    AdventureWorks 데이터베이스를 설치하는 방법에 대한 자세한 내용은 [연습: AdventureWorks 데이터베이스 설치](http://go.microsoft.com/fwlink/?LinkID=65819)를 참조하세요.  
  
-   이 설명서의 거의 모든 코드 예제는 명령줄에서 실행하기 위한 것으로, 모든 코드 예제의 자동화된 테스트를 사용할 수 있습니다. 명령줄에서 PHP를 실행하는 방법에 대한 자세한 내용은 [Using PHP from the command line(명령줄에서 PHP 사용)](http://php.net/manual/en/features.commandline.php)을 참조하세요.  
  
-   명령줄에서 예제를 실행하도록 작성한 경우에도 스크립트를 변경하지 않고 브라우저에서 각 예제를 호출하여 실행할 수 있습니다. 를 달성 하기 위해 출력을 보기 좋게으로 각 "\n" 대체 "\<\/b r >" 브라우저에서 호출 하기 전에 각 예제에 합니다.  
  
-   각각의 예제에 중점을 두기 위해 오류 수정 처리가 모든 예제에서 수행되지는 않습니다. 응용 프로그램의 필요에 따라 **sqlsrv** 함수 또는 PDO 메서드를 호출하여 오류를 검사하고 처리하는 것이 좋습니다.  
  
    오류가 발생하는 경우 오류 정보를 얻는 쉬운 방법은 다음 코드 줄을 사용하여 스크립트를 종료하는 것입니다.  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    또는 PDO를 사용하는 경우  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    오류 및 경고 처리에 대한 자세한 내용은 [오류 및 경고 처리](../../connect/php/handling-errors-and-warnings.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[PHP SQL 드라이버 개요](../../connect/php/overview-of-the-php-sql-driver.md)
  

