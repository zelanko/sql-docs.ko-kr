---
title: setNull 메서드 (int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c74e06-2858-49ba-bae7-b88808e5fff4
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 62f91e694ea655fe29c7306aeea9471ba432072d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800342"
---
# <a name="setnull-method-int-int-javalangstring"></a>setNull 메서드(int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정할 매개 변수의 형식 및 이름이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNull(int paramIndex,  
                          int sqlType,  
                          java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *paramIndex*  
  
 매개 변수 번호를 나타내는 **int**입니다.  
  
 *sqlType*  
  
 java.sql.Types로 정의된 JDBC 형식 코드입니다.  
  
 *typeName*  
  
 설정할 매개 변수의 정규화된 이름을 나타내는 **String**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setNull 메서드는 java.sql.PreparedStatement 인터페이스의 setNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNull 메서드(SQLServerPreparedStatement)](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
