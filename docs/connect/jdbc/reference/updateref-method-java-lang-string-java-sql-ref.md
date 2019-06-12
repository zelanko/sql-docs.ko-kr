---
title: updateRef 메서드(java.lang.String, java.sql.Ref) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateRef (java.lang.String, java.sql.Ref)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7740d17d-282f-4f1d-91f9-c68a873b069a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a07f14422a1e4d6db9c9715ac766b9265fdeb86c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778463"
---
# <a name="updateref-method-javalangstring-javasqlref"></a>updateRef 메서드(java.lang.String, java.sql.Ref)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 이름이 지정된 경우 지정된 열을 java.sql.Ref 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateRef(java.lang.String columnName,  
                      java.sql.Ref x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *x*  
  
 Ref 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateInt 메서드는 java.sql.ResultSet 인터페이스의 updateInt 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateRef 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
