---
title: getTime 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getClob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 91020fad-a9e2-4ea4-9c72-c63cf6b1051c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf2d7c17d640db8986669b70048e67f3f32b6ac0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798104"
---
# <a name="getclob-method-int-sqlserverresultset"></a>getClob 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 Clob 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Clob getClob(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 Clob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getByte 메서드는 java.sql.ResultSet 인터페이스의 getByte 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateNClob 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
