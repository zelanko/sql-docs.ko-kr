---
title: next 메서드 (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.next
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 60248447-6908-4036-a779-a501453cd553
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c893fcb4ee536c3a84ebab87a5092f9c884afe35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="next-method-sqlserverresultset"></a>next 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서를 현재 위치에서 한 행 아래로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean next()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 새 현재 행이 유효 합니다. **false** 처리할 행이 더 이상 없는 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 다음이 메서드는 java.sql.ResultSet 인터페이스에는 다음 메서드에 의해 지정 됩니다.  
  
 처음에는 결과 집합 커서가 첫 번째 행 앞에 놓입니다. 다음 방법으로 첫 번째 호출이 첫 번째 행을 현재 행으로 만듭니다, 그리고 두 번째 호출 하면 두 번째 행이 현재 행 및 등입니다.  
  
 입력된 스트림을 현재 행에 대 한 열려 있으면 다음 방법에 대 한 호출은 암시적으로 닫습니다. 에 대 한 경고 체인이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체는 새 행을 읽을 때 삭제 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
