---
title: supportsLimitedOuterJoins 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsLimitedOuterJoins
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 06225a1a-a58d-4bff-b2ef-be303f051644
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8e1b235a8c779c652a8678802bbb91a1de83f38
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67969304"
---
# <a name="supportslimitedouterjoins-method-sqlserverdatabasemetadata"></a>supportsLimitedOuterJoins 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 외부 조인을 제한적으로 지원하는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsLimitedOuterJoins()  
```  
  
## <a name="return-value"></a>반환 값  
 지원 되는 경우 **true** 입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsLimitedOuterJoins 메서드는 supportsLimitedOuterJoins 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
