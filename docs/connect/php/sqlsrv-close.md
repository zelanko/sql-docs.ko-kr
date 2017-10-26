---
title: sqlsrv_close | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- sqlsrv_close
apitype: NA
helpviewer_keywords:
- sqlsrv_close
- API Reference, sqlsrv_close
ms.assetid: 6ac6209c-a134-4f8f-b88b-8eefaa1cbc7f
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ab9135195867a02dccf3885b551ab2a1f4f5ebb1
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrvclose"></a>sqlsrv_close
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

지정된 연결을 닫고 연결된 리소스를 해제합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sqlsrv_close( resource $conn )  
```  
  
#### <a name="parameters"></a>매개 변수  
*$conn*: 닫히는 연결입니다.  
  
## <a name="return-value"></a>반환 값  
잘못된 매개 변수를 사용하여 함수를 호출하지 않는 한 부울 값 **true** 입니다. 잘못된 매개 변수를 사용하여 함수를 호출하는 경우에는 **false** 가 반환됩니다.  
  
> [!NOTE]  
> **Null** 은 이 함수에 대해 유효한 매개 변수입니다. 그러면 스크립트에서 함수가 여러 번 호출될 수 있습니다. 예를 들어 오류 조건에서 연결을 닫고 스크립트 끝에서 다시 닫는 경우 두 번째 호출에서를 **sqlsrv_close** 돌아갑니다 **true** 에 첫 번째 호출 하므로 **sqlsrv_ 닫기** (오류 조건)를 설정 하는 연결 리소스 **null**합니다.  
  
## <a name="example"></a>예제  
다음 예제에서는 연결을 닫습니다. 이 예제에서는 SQL Server가 로컬 컴퓨터에 설치된 것으로 가정합니다. 명령줄에서 예제가 실행될 때 모든 출력은 콘솔에 기록됩니다.  
  
```  
<?php  
/*Connect to the local server using Windows Authentication and   
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$conn = sqlsrv_connect( $serverName);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
//-----------------------------------------------  
// Perform operations with connection here.  
//-----------------------------------------------  
  
/* Close the connection. */  
sqlsrv_close( $conn);  
echo "Connection closed.\n";  
?>  
```  
  
## <a name="see-also"></a>참고 항목  
[SQLSRV 드라이버 API 참조](../../connect/php/sqlsrv-driver-api-reference.md)  
[설명서의 코드 예제 정보](../../connect/php/about-code-examples-in-the-documentation.md)  
  

