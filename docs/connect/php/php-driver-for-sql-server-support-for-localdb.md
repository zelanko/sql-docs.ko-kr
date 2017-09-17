
---
title: PHP Driver for SQL Server Support for LocalDB | Microsoft Docs
ms.custom: 
ms.date: 02/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a54071c75ca4437974be7b742ee3285972850e0a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="php-driver-for-sql-server-support-for-localdb"></a>PHP Driver for SQL Server Support for LocalDB(PHP Driver for SQL Server의 LocalDB 지원)

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

부터는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]의 경량 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], LocalDB 라고 부르는, 사용할 수 있습니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.

## <a name="remarks"></a>주의

LocalDB 설치 및 LocalDB 인스턴스를 구성 하는 방법을 비롯 한 LocalDB에 대 한 자세한 내용은 참조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 온라인 설명서 항목 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB 합니다.

요약하자면, LocalDB를 통해 다음과 같은 기능을 수행할 수 있습니다.

-   **sqllocaldb.exe i** 를 사용하여 기본 인스턴스의 이름을 확인할 수 있습니다.

-   **AttachDBFilename** 연결 문자열 키워드를 사용하여 서버가 연결해야 하는 데이터베이스 파일을 지정할 수 있습니다. **AttachDBFilename**을 사용할 때 **Database** 연결 문자열 키워드를 사용하여 데이터베이스 이름을 지정하지 않으면 응용 프로그램이 닫힐 때 LocalDB 인스턴스에서 데이터베이스가 제거됩니다.

-   연결 문자열에 LocalDB 인스턴스를 지정 합니다. 예를 들어 다음은 샘플 SQLSRV 연결 문자열이입니다.

    ```php
    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array( 'Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF','Database'=>'myData'));

    $conn = sqlsrv_connect( '(localdb)\\v11.0',
        array('AttachDBFileName'=>'c:\\myData.MDF'));
    ```

    다음은 샘플 PDO_SQLSRV 연결 문자열:  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. `sqlcmd -S (localdb)\v11.0`)을 입력합니다. (; 명령줄에서 실행할 때와 동일한 결과 얻기 위해 올바른 계정으로 실행 해야 하는 IIS를 실행 하는 경우 참조 [2 부 전체 iis를 사용 하 여 LocalDB: 인스턴스 소유권](http://blogs.msdn.com/b/sqlexpress/archive/2011/12/09/using-localdb-with-full-iis-part-2-instance-ownership.aspx) 자세한 정보에 대 한 합니다.)

연결 문자열 예 SQLSRV 드라이버를 사용 하 여 명명 된 인스턴스 myinstance LocalDB에서 데이터베이스에 연결 하는 다음과 같습니다.

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

연결 문자열 예 PDO_SQLSRV 드라이버를 사용 하 여 명명 된 인스턴스 myinstance LocalDB에서 데이터베이스에 연결 하는 다음과 같습니다.  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

LocalDB를 다운로드할 수 있습니다는 [SQL Server 2012 기능 팩 페이지](http://go.microsoft.com/fwlink/?LinkID=236805), 또는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express edition. sqlcmd 할 데이터를 수정 하 여 LocalDB 인스턴스에서 sqlcmd.exe를 사용 하는 경우 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)], 명령줄 유틸리티 다운로드에서에서 얻을 수는 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 기능 팩 페이지.

## <a name="see-also"></a>관련 항목:

[서버에 연결](../../connect/php/connecting-to-the-server.md)

