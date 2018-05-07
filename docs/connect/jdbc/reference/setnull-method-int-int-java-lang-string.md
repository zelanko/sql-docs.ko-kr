---
title: setNull 메서드 (int, int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setNull (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43c74e06-2858-49ba-bae7-b88808e5fff4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a34ce8e9c268e810c09b6f39d940d27df866a3a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
 **int** 매개 변수 수를 나타내는입니다.  
  
 *SQLtype*  
  
 java.sql.Types로 정의된 JDBC 형식 코드입니다.  
  
 *typeName*  
  
 A **문자열** 설정 되는 매개 변수의 정규화 된 이름을 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 setNull 메서드는 java.sql.PreparedStatement 인터페이스의 setNull 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [setNull 메서드 &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
