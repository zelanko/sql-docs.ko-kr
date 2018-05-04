---
title: executeUpdate 메서드 (java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c52a20e-527e-4d14-9a5a-4cd195aac8ed
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c173fa5ed1c2d431038cb6ffd8b917d1d521e27
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
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
  
 SQL 문이 포함된 **문자열**입니다.  
  
 *flag*  
  
 **int** 경우 자동 생성 키 허용할지를 나타내는 값입니다. 다음 상수 중 하나이야 합니다.  
  
 RETURN_GENERATED_KEYS  
  
 NO_GENERATED_KEYS  
  
## <a name="return-value"></a>반환 값  
 **int** DDL 문을 사용 하는 경우 0, 영향을 받는 행의 수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 executeUpdate 메서드는 java.sql.Statement 인터페이스의 executeUpdate 메서드에 의해 지정 됩니다.  
  
 업데이트 횟수가 1보다 크거나 둘 이상의 결과 집합을 생성하는 저장 프로시저 결과를 실행하는 경우 [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) 메서드를 사용하여 저장 프로시저를 실행합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [executeUpdate 메서드 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
