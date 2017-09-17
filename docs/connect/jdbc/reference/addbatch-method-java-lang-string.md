---
title: "addBatch 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerPreparedStatement.addBatch (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 093f6c3b-49a6-4043-9993-bd0482de04dd
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8febab83df94f0d1f6034c133cdd7e5a95db51ad
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="addbatch-method-javalangstring"></a>addBatch 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 대 한 명령의 현재 목록에 지정된 된 SQL 명령을 추가 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void addBatch(java.lang.String sql)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 addBatch 메서드는 java.sql.Statement 인터페이스의 addBatch 메서드에 의해 지정 됩니다.  
  
 이 메서드를 호출 개체가 만들어질 때 SQLServerPreparedStatement 개체에 대 한 SQL 문이 지정 된 후 예외가 발생 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [addBatch 메서드 &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
