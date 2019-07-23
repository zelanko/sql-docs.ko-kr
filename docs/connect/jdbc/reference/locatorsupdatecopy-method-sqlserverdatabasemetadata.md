---
title: locatorsUpdateCopy 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.locatorsUpdateCopy
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6ec8c1d-7ff8-4bc5-8bd3-0199a9294a6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e9e800c326f18b5247d1257431bb2243ad00c57
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976839"
---
# <a name="locatorsupdatecopy-method-sqlserverdatabasemetadata"></a>locatorsUpdateCopy 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  LOB에 대한 업데이트가 복사본에서 수행되는지 아니면 LOB에 직접 수행되는지를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean locatorsUpdateCopy()  
```  
  
## <a name="return-value"></a>반환 값  
 복사본이 업데이트 되 면 **true** 입니다. 업데이트를 직접 수행 하는 경우 **false** 입니다.  
  
## <a name="exceptions"></a>예외  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 이 locatorsUpdateCopy 메서드는 locatorsUpdateCopy 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
