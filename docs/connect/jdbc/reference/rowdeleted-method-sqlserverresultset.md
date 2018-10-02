---
title: rowDeleted 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b99e2f6f7bc289e123c36e3a528ec937e0f5f7ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605611"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  행이 삭제되었는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>반환 값  
 행이 삭제되었고 삭제 내용이 검색되면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 rowDeleted 메서드는 java.sql.ResultSet 인터페이스의 rowDeleted 메서드에 의해 지정 됩니다.  
  
 삭제된 행은 결과 집합에 가시적인 빈틈을 남겨 둘 수 있습니다. 이 메서드를 사용하면 결과 집합에서 빈틈을 검색할 수 있습니다. 반환되는 값은 이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체가 삭제 내용을 검색할 수 있는지 여부에 따라 달라집니다.  
  
> [!NOTE]  
>  검색이 정방향 및 동적 커서에 대해 일시적이기는 하지만 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 업데이트 가능한 모든 커서 유형에 대해 삭제된 행을 검색합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
