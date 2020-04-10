---
title: relative 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f9233d6e4224e33d9d9c71b1352a792ba19cff2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904063"
---
# <a name="relative-method-sqlserverresultset"></a>relative 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행을 기준으로 지정된 행 수만큼 커서를 양의 방향 또는 음의 방향으로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *nRows*  
  
 이동할 행 수를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 커서가 행에 있으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 relative 메서드는 java.sql.ResultSet 인터페이스의 relative 메서드에 의해 지정됩니다.  
  
 결과 집합의 첫 번째 또는 마지막 행을 지나 이동하려고 하면 커서가 첫 번째 행의 앞이나 마지막 행의 뒤에 놓입니다. `relative(0)`를 호출할 수는 있지만 이 경우 커서 위치가 변경되지 않습니다.  
  
 `relative(1)` 메서드를 호출하는 것은 [next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) 메서드를 호출하는 것과 같습니다. `relative(-1)` 메서드를 호출하는 것은 [previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) 메서드를 호출하는 것과 같습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
