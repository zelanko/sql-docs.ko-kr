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
ms.openlocfilehash: 9f7e87040fa74954435ed52f9923568e8bfed3fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954924"
---
# <a name="execute-method-"></a>execute 메서드()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체에서 모든 종류의 SQL 문을 실행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean execute()  
```  
  
## <a name="return-value"></a>반환 값  
 문에서 결과 집합을 반환 하면 **true** 입니다. 업데이트 횟수가 반환 되거나 결과가 반환 되지 않으면 **false** 입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 execute 메서드는 java.sql.PreparedStatement 인터페이스의 execute 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [execute 메서드&#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
