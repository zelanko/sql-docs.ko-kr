---
title: executeUpdate 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 059f463c6a448c6ae2ab302542a50cde1f533db8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67954708"
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate 메서드(java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 SQL 문을 실행하고 지정된 배열에 표시된 자동 생성 키를 검색에 사용해야 하는지 여부를 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에 알립니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
 *columnIndexes*  
  
 자동 생성 키의 열 인덱스를 사용할 수 있도록 해야 하는지 여부를 나타내는 int의 배열입니다.  
  
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
  
  
