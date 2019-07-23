---
title: updateLong 메서드 (int, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (int, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6363288-1415-4b25-8bb3-c34d6211c6d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8e8d0ad2332d1990445b8c6fb3c1ebd5914453d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998811"
---
# <a name="updatelong-method-int-long"></a>updateLong 메서드(int, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정된 경우 지정된 열을 **long** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateLong(int index,  
                       long x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 **Long** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateLong 메서드는 java.sql.ResultSet 인터페이스의 updateLong 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateLong 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
