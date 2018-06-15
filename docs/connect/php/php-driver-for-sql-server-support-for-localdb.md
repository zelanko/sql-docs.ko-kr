---
title: LocalDB에 대 한 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 438802c4645ff3acdc1bed42af22e4e32786e1d0
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308752"
---
# <a name="support-for-localdb"></a>LocalDB에 대 한 지원

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB는 경량 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 를 사용할 수 있었던 이후 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]합니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.

## <a name="remarks"></a>Remarks

LocalDB 설치 및 LocalDB 인스턴스를 구성 하는 방법을 비롯 한 LocalDB에 대 한 자세한 내용은 참조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에 온라인 설명서 항목 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] Express LocalDB 합니다.

간단히 말해서 LocalDB 할 수 있습니다.

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

LocalDB를 설치 하는 방법에 지침은 참조는 [LocalDB 설명서](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)합니다. Sqlcmd.exe를 사용 하 여 LocalDB 인스턴스에서 데이터를 수정 하는 경우는 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)합니다.

## <a name="see-also"></a>관련 항목

[서버에 연결](../../connect/php/connecting-to-the-server.md)
