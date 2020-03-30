---
title: isAfterLast 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.isAfterLast
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 19f9d124-3184-4985-8b97-503a8ab8b4f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 233599694c4fb4f7764bbb48d5c77e0fcd273340
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67977842"
---
# <a name="isafterlast-method-sqlserverresultset"></a>isAfterLast 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  커서가 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 마지막 행 뒤에 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isAfterLast()  
```  
  
## <a name="return-value"></a>Return Value  
 커서가 마지막 행 뒤에 있으면 **true**입니다. 커서가 그 외의 위치에 있거나 결과 집합에 행이 들어 있지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 isAfterLast 메서드는 java.sql.ResultSet 인터페이스의 isAfterLast 메서드에 의해 지정됩니다.  
  
 이 메서드를 정방향 전용의 읽기 전용 커서를 비롯한 동적 커서와 함께 사용할 경우 selectMethod 연결 속성이 "cursor"로 설정되어 있으면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
