---
title: getMoreResults 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08760680774b2e760b66d9e210c4ef939872444e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981768"
---
# <a name="getmoreresults-method-int"></a>getMoreResults 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체의 다음 결과로 이동하고 지정된 모드의 지침에 따라 현재 열려 있는 결과 집합 개체를 처리합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *mode*  
  
 현재 열려 있는 결과 집합 개체의 처리 방법을 나타내는 **int**입니다. 다음 상수 중 하나여야 합니다.  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT(JDBC 드라이버에서는 지원되지 않음)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Return Value  
 반환된 결과가 결과 집합이면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getMoreResults 메서드는 java.sql.Statement 인터페이스의 getMoreResults 메서드에 의해 지정됩니다.  
  
 결과가 검색되기 전에 getMoreResults 메서드를 호출할 경우 이 메서드는 *mode* 인수에 지정된 대로 동작하고 다음 결과로 이동합니다.  
  
> [!NOTE]  
>  JDBC 드라이버에서는 KEEP_CURRENT_RESULT 상수의 사용을 지원하지 않습니다. 이 상수를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getMoreResults 메서드(SQLServerStatement)](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
