---
title: cancel 메서드 (SQLServerStatement) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5df32b6de96c310f0be3d936a48c3544e1132df
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="cancel-method-sqlserverstatement"></a>cancel 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 실행 되 고 있는 SQL 문을 취소 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 cancel 메서드는 java.sql.Statement 인터페이스의 취소 메서드에 의해 지정 됩니다.  
  
 크기가 큰 정방향 전용의 읽기 전용 결과 집합을 하나만 생성하는 문을 실행할 경우 반환된 결과 집합에 포함된 처음 몇 개의 행에만 관심이 있는 경우가 있습니다. 이 경우 응용 프로그램이 호출할 수는 [취소](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) 메서드 결과 닫기 전에 관련된 문 개체의 나머지 불필요 한 행을 삭제 하는 데 필요한 처리 시간을 최소화 하기 위해 설정 합니다. 이 기술을 사용할지 여부를 결정할 때는 절약되는 처리 시간과 서버에서 실행을 취소하는 데 필요한 시간 및 추가 왕복을 적절히 고려해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
