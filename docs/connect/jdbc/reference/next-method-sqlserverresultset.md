---
title: next 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8fcd3125f45622ddd167acf06ed91ccffb02a3b5
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779526"
---
# <a name="next-method-sqlserverresultset"></a>next 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 현재 위치에서 한 행 아래로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 을 새 현재 행이 유효 합니다. **false** 처리할 행이 더 이상 없으면입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 next 메서드는 java.sql.ResultSet 인터페이스의 next 메서드에 의해 지정됩니다.  
  
 처음에는 결과 집합 커서가 첫 번째 행 앞에 놓입니다. next 메서드를 처음으로 호출하면 첫 번째 행이 현재 행이 되고 두 번째로 이 메서드를 호출하면 두 번째 행이 현재 행이 되는 방식으로 처리됩니다.  
  
 현재 행에 대해 입력 스트림이 열려 있는 경우 next 메서드를 호출하면 해당 스트림이 암시적으로 닫힙니다. 새 행을 읽을 때는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체에 대한 경고 체인이 지워집니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
