---
title: SQLServerException 클래스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cfcc73705d04b3d3efa7515f74676b0eda120323
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680282"
---
# <a name="sqlserverexception-class"></a>SQLServerException 클래스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  실패하거나 완료되지 않은 SQL 문 실행을 나타냅니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.sql.SQLException  
  
 **구현:** java.io.Serializable  
  
## <a name="syntax"></a>구문  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerException 클래스는 SQL 92 및 XOPEN 상태 코드를 처리합니다. 이러한 상태 코드는 사용자가 지정한 연결 속성을 사용하여 전환할 수 있습니다. 예외는 열려 있는 지정된 로그 파일에 기록됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerException 멤버](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
