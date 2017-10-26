---
title: "executeUpdate 메서드 (java.lang.String, int) | Microsoft Docs"
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
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bb27e4538eccf87257d16555505442f76461adb0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 메서드(java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  주어진 신호 및 SQL 문을 실행는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 여부 키 자동으로 생성 하는 방법에 대 한 지정 된 플래그로이 의해 생성 된 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체 검색에 사용할 수 있어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 A **문자열** SQL 문이 들어 있는입니다.  
  
 *플래그*  
  
 **int** 경우 자동 생성 키 허용할지를 나타내는 값입니다. 다음 상수 중 하나이야 합니다.  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>반환 값  
 **int** DDL 문을 사용 하는 경우 0, 영향을 받는 행의 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 executeUpdate 메서드는 java.sql.Statement 인터페이스의 executeUpdate 메서드에 의해 지정 됩니다.  
  
 1 보다 큰 또는 둘 이상의 결과 집합을 사용 하 여 생성 하 여 업데이트 횟수로 인해 저장된 프로시저를 실행 하는 경우는 [실행](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 저장된 프로시저를 실행 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [executeUpdate 메서드 &#40; SQLServerStatement &#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

