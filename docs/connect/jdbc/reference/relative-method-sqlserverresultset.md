---
title: relative 메서드 (SQLServerResultSet) | Microsoft Docs
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
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d210c40ac0c288ef57e74f37218515e21148fdb3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="relative-method-sqlserverresultset"></a>relative 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행을 기준으로 지정된 행 수만큼 커서를 양의 방향 또는 음의 방향으로 이동합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *nRows*  
  
 **int** 이동할 행 수를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 커서가 행에 있는 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 상대이 메서드는 java.sql.ResultSet 인터페이스의 상대 메서드에 의해 지정 됩니다.  
  
 결과 집합의 첫 번째 또는 마지막 행을 지나 이동하려고 하면 커서가 첫 번째 행의 앞이나 마지막 행의 뒤에 놓입니다. 호출 `relative(0)` 유효 하지만 커서 위치가 변경 되지 않습니다.  
  
 메서드를 호출 하면 `relative(1)` 는 호출 하는 [다음](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) 메서드. 메서드를 호출 하면 `relative(-1)` 는 호출 하는 [이전](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
