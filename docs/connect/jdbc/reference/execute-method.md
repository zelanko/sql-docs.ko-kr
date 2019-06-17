---
title: execute 메서드 () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.execute ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa96d0f8-101b-422f-a767-405be9a5f74f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7050a26a8fe98d5069cd52a58afe501bee738499
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802321"
---
# <a name="execute-method-"></a>execute 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체에서 모든 종류의 SQL 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean execute()  
```  
  
## <a name="return-value"></a>반환 값  
 **true** 문에서 결과 집합을 반환 합니다. **false** 업데이트 횟수 또는 없는 결과 반환 하는 경우.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 execute 메서드는 java.sql.PreparedStatement 인터페이스의 execute 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [execute 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
