---
title: LocalDB에 대한 PHP 드라이버 지원
description: Microsoft Drivers for PHP for SQL Server에서 LocalDB 데이터베이스 인스턴스에 대한 연결을 지원하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d315ad6a-0d50-4093-80c2-2f11217237c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d618706cd05796079904c971cdf7b0c32485c1d4
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886290"
---
# <a name="support-for-localdb"></a>LocalDB 지원

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

LocalDB는 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 사용 가능해진 경량 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]입니다. 이 항목에서는 LocalDB 인스턴스의 데이터베이스에 연결하는 방법에 대해 설명합니다.

## <a name="remarks"></a>설명

LocalDB 설치 및 LocalDB 인스턴스 구성 방법을 포함하여 LocalDB에 대한 자세한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Express LocalDB의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서 항목을 참조하세요.

요약하자면, LocalDB를 통해 다음과 같은 기능을 수행할 수 있습니다.

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

    다음은 PDO_SQLSRV 연결 문자열의 예제입니다.  

    ```php
    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'Database=myData', NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF;Database=myData ',
        NULL, NULL);

    $conn = new PDO( 'sqlsrv:server=(localdb)\\v11.0;'
        . 'AttachDBFileName=c:\\myData.MDF', NULL, NULL);  
    ```

필요한 경우 sqllocaldb.exe를 사용하여 LocalDB 인스턴스를 만들 수 있습니다. 또한 sqlcmd.exe를 사용하여 LocalDB 인스턴스에서 데이터베이스를 추가하고 수정할 수 있습니다. `sqlcmd -S (localdb)\v11.0`)을 입력합니다. (IIS에서 실행하는 경우 올바른 계정으로 실행해야 명령줄에서 실행할 때와 동일한 결과를 얻을 수 있습니다. 자세한 내용은 [전체 IIS로 LocalDB 사용하기(2부): 인스턴스 소유권](/archive/blogs/sqlexpress/using-localdb-with-full-iis-part-2-instance-ownership)을 참조하세요.)

다음은 myInstance이라는 LocalDB 명명 인스턴스의 데이터베이스에 연결되는 SQLSRV 드라이버를 사용하는 연결 문자열의 예입니다.

```php
$conn = sqlsrv_connect( '(localdb)\\myInstance',
    array( 'Database'=>'myData'));
```

다음은 myInstance이라는 LocalDB 명명 인스턴스의 데이터베이스에 연결되는 PDO_SQLSRV 드라이버를 사용하는 연결 문자열의 예입니다.  
  
```php
$conn = new PDO( 'sqlsrv:server=(localdb)\\myInstance;'
    . 'database=myData', NULL, NULL);
```

LocalDB 설치 관련 지침은 [LocalDB 설명서](../../database-engine/configure-windows/sql-server-2016-express-localdb.md)를 참조하세요. sqlcmd.exe를 사용하여 LocalDB 인스턴스의 데이터를 수정하는 경우에는 [sqlcmd 유틸리티](../../tools/sqlcmd-utility.md)가 필요합니다.

## <a name="see-also"></a>참고 항목

[서버에 연결](../../connect/php/connecting-to-the-server.md)
