---
title: supportsMultipleResultSets 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMultipleResultSets
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cb4d0b91-db1d-4a6f-a87c-8ea125215afc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 688d17b7f703dc34658e66e3915b8ffaeda24e7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969220"
---
# <a name="supportsmultipleresultsets-method-sqlserverdatabasemetadata"></a>supportsMultipleResultSets 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) 클래스의 [execute](../../../connect/jdbc/reference/execute-method.md) 메서드를 한 번 호출하여 여러 개의 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체를 가져올 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsMultipleResultSets()  
```  
  
## <a name="return-value"></a>반환 값  
 지원 되는 경우 **true** 입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsMultipleResultSets 메서드는 supportsMultipleResultSets 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
