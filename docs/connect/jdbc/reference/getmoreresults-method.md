---
title: "getMoreResults 메서드 () | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8259b562590d21c57f0780260f50bf15032a7ead
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getmoreresults-method-"></a>getMoreResults 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 항목의 다음 결과로 이동 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 경우 반환 된 결과 결과 집합입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getMoreResults 메서드는 java.sql.Statement 인터페이스의 getMoreResults 메서드에 의해 지정 됩니다.  
  
 현재 열려 있는 결과 집합 개체를 사용 하 여 가져온 닫습니다 getMoreResults 메서드를 암시적으로 호출 된 [getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) 메서드.  
  
## <a name="see-also"></a>관련 항목:  
 [getMoreResults 메서드 &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

