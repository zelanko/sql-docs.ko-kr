---
title: 설명서의 코드 예제 정보 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc76cee723c11d49a4d6149a7c3a1df4cedbc256
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015175"
---
# <a name="about-code-examples-in-the-documentation"></a>설명서의 코드 예제 정보
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>코드 예제에 대한 설명
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 설명서의 코드 예제를 실행할 때 몇 가지 유의 사항이 있습니다.  
  
-   거의 모든 예제에서 SQL Server 2008 이상과 AdventureWorks 데이터베이스가 로컬 컴퓨터에 설치되어 있다고 가정합니다.  
  
    SQL Server 무료 버전 및 평가판 버전을 다운로드하는 방법에 대한 자세한 내용은 [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193)를 참조하세요.  
  
    AdventureWorks 데이터베이스를 다운로드하고 설치하는 방법에 관한 정보는 [SQL Server Samples Github 리포지토리의 AdventureWorks 페이지](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)를 참조하세요.
  
-   이 설명서의 거의 모든 코드 예제는 명령줄에서 실행하기 위한 것으로, 모든 코드 예제의 자동화된 테스트를 사용할 수 있습니다. 명령줄에서 PHP를 실행하는 방법에 대한 자세한 내용은 [Using PHP from the command line(명령줄에서 PHP 사용)](https://php.net/manual/en/features.commandline.php)을 참조하세요.  
  
-   명령줄에서 예제를 실행하도록 작성한 경우에도 스크립트를 변경하지 않고 브라우저에서 각 예제를 호출하여 실행할 수 있습니다. 출력의 형식을 보기 좋게 하려면 브라우저에서 예제를 호출하기 전에 예제에서 각 "\n"을 "\<\/br>"로 바꿉니다.  
  
-   각각의 예제에 중점을 두기 위해 오류 수정 처리가 모든 예제에서 수행되지는 않습니다. 애플리케이션의 필요에 따라 **sqlsrv** 함수 또는 PDO 메서드를 호출하여 오류를 검사하고 처리하는 것이 좋습니다.  
  
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
[Microsoft Drivers for PHP for SQL Server 개요](../../connect/php/overview-of-the-php-sql-driver.md)
  
