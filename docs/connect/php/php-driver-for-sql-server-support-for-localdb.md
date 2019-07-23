---
title: LocalDB 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f6da7f1aed956c8b2f5c71496c9c121f6006eabb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935955"
---
# <a name="support-for-localdb"></a>LocalDB 지원

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB는 이후 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]사용 가능한 경량 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전입니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.

## <a name="remarks"></a>Remarks

Localdb 설치 및 localdb 인스턴스 구성 방법을 비롯 한 localdb에 대 한 자세한 내용은 Express localdb의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 온라인 설명서 항목을 참조 하십시오.

간단히 LocalDB를 사용 하면 다음을 수행할 수 있습니다.

-   **sqllocaldb.exe i** 를 사용하여 기본 인스턴스의 이름을 확인할 수 있습니다.

-   **AttachDBFilename** 연결 문자열 키워드를 사용하여 서버가 연결해야 하는 데이터베이스 파일을 지정할 수 있습니다. **AttachDBFilename**을 사용할 때 **Database** 연결 문자열 키워드를 사용하여 데이터베이스 이름을 지정하지 않으면 애플리케이션이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.

-   연결 문자열에 LocalDB 인스턴스를 지정합니다. 예를 들어 샘플 SQLSRV 연결 문자열은 다음과 같습니다.

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    다음은 샘플 PDO_SQLSRV 연결 문자열입니다.  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. `sqlcmd -S (localdb)\v11.0`)을 입력합니다. (IIS에서 실행 하는 경우 명령줄에서 실행 하는 경우와 동일한 결과를 얻으려면 올바른 계정으로 실행 해야 합니다. 자세한 내용은 [전체 IIS를 사용 하는 LocalDB 사용, 2 부: 인스턴스 소유권](https://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) 을 참조 하세요.)

다음은 myInstance 이라는 LocalDB 명명 된 인스턴스의 데이터베이스에 연결 하는 SQLSRV 드라이버를 사용 하는 연결 문자열의 예입니다.

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

다음은 PDO_SQLSRV 드라이버를 사용 하 여 myInstance 라는 LocalDB 명명 된 인스턴스에 있는 데이터베이스에 연결 하는 연결 문자열의 예입니다.  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

LocalDB 설치에 대 한 지침은 [localdb 설명서](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)를 참조 하세요. Sqlcmd를 사용 하 여 LocalDB 인스턴스에서 데이터를 수정 하는 경우 [sqlcmd 유틸리티가](../../tools/sqlcmd-utility.md)필요 합니다.

## <a name="see-also"></a>참고 항목

[서버에 연결](../../connect/php/connecting-to-the-server.md)
