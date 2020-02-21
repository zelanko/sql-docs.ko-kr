---
title: getAsciiStream 메서드(SQLServerClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getAsciiStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 134abe5e-5add-4d27-b333-b4b0f4d94c31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfa7ed5314d75ba0bec0d2a000575e8d9ed4d3fc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67954132"
---
# <a name="getasciistream-method-sqlserverclob"></a>getAsciiStream 메서드(SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  CLOB을 ASCII 스트림으로 구체화합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>Return Value  
 CLOB 데이터가 들어 있는 입력 스트림입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getAsciiStream 메서드는 java.sql.Clob 인터페이스의 getAsciiStream 메서드에 의해 지정됩니다.  
  
 항상 바이트 배열을 반환하며, CLOB의 데이터가 유니코드인지 아니면 다른 멀티바이트 코드 페이지인지를 알 수 있는 방법이 없으므로 이 데이터가 ASCII 형식이라고 가정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
