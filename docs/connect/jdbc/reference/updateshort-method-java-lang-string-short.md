---
title: updateShort 메서드 (java.lang.String, short) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateShort (java.lang.String, short)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e596e99-11ce-4a57-b247-e40078922036
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2627346946fe7ebcb7d361eeaf28cb0fe56df16e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813297"
---
# <a name="updateshort-method-javalangstring-short"></a>updateShort 메서드(java.lang.String, short)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 이름이 지정된 경우 지정된 열을 **short** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateShort(java.lang.String columnName,  
                        short x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *x*  
  
 A **짧은** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getShort 메서드는 java.sql.ResultSet 인터페이스의 getShort 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateShort 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
