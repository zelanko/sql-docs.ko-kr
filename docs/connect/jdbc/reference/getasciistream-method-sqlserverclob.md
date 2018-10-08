---
title: getAsciiStream 메서드 (SQLServerClob) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2490fc903f7c1c509adc1e6f776f00a39e5f4616
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767271"
---
# <a name="getasciistream-method-sqlserverclob"></a>getAsciiStream 메서드(SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  CLOB을 ASCII 스트림으로 구체화합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getAsciiStream()  
```  
  
## <a name="return-value"></a>반환 값  
 CLOB 데이터가 들어 있는 입력 스트림입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getAsciiStream 메서드는 java.sql.Clob 인터페이스의 getAsciiStream 메서드에 의해 지정 됩니다.  
  
 항상 바이트 배열을 반환하며, CLOB의 데이터가 유니코드인지 아니면 다른 멀티바이트 코드 페이지인지를 알 수 있는 방법이 없으므로 이 데이터가 ASCII 형식이라고 가정합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerClob 메서드](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob 멤버](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob 클래스](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
