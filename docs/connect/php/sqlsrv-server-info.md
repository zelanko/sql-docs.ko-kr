---
title: sqlsrv_server_info | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_server_info
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_server_info
- sqlsrv_server_info
ms.assetid: ef6fe2b7-d267-4379-b948-5626c4684367
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0831addcaec34e24d12f3b775125f7414e302b8f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928536"
---
# <a name="sqlsrv_server_info"></a>sqlsrv_server_info
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

서버에 대한 정보를 반환합니다. 이 함수를 호출하기 전에 연결을 설정해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_server_info( resource $conn)  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: 클라이언트 및 서버를 연결하는 연결 리소스입니다.  
  
## <a name="return-value"></a>Return Value  
다음 키를 사용하는 결합형 배열입니다.  
  
|키|Description|  
|-------|---------------|  
|CurrentDatabase|현재 대상이 되는 데이터베이스입니다.|  
|SQLServerVersion|SQL Server의 버전입니다.|  
|SQLServerName|서버 이름|  
  
## <a name="example"></a>예제  
다음 예제에서는 명령줄에서 예제가 실행될 때 서버 정보를 콘솔에 씁니다.  
  
```  
<?php  
/* Connect to the local server using Windows Authentication. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
$server_info = sqlsrv_server_info( $conn);  
if( $server_info )  
{  
      foreach( $server_info as $key => $value)  
      {  
             echo $key.": ".$value."\n";  
      }  
}  
else  
{  
      echo "Error in retrieving server info.\n";  
      die( print_r( sqlsrv_errors(), true));  
}  
  
/* Free connection resources. */  
sqlsrv_close( $conn);  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  

[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  
