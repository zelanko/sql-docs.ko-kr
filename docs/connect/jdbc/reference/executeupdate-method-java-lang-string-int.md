---
title: executeUpdate 메서드(java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783058a764963637f2c91808424bac7bdd403c02
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954752"
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 메서드(java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 SQL 문을 실행하고 이 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체에서 생성된 자동 생성 키를 검색에 사용할 수 있도록 해야 하는지 여부를 지정된 플래그로 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int flag)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
 *flag*  
  
 자동 생성 키를 사용할 수 있도록 해야 하는지 여부를 나타내는 **int** 값입니다. 다음 상수 중 하나이야 합니다.  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>Return Value  
 영향을 받는 행 수를 나타내는 **int**이며, DDL 문을 사용하는 경우에는 0입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 executeUpdate 메서드는 java.sql.Statement 인터페이스의 executeUpdate 메서드에 의해 지정됩니다.  
  
 업데이트 횟수가 1보다 크거나 둘 이상의 결과 집합을 생성하는 저장 프로시저 결과를 실행하는 경우 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용하여 저장 프로시저를 실행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [executeUpdate 메서드&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
