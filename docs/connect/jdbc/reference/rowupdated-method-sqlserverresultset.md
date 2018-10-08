---
title: rowUpdated 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40afdf8854e40050e718b9c456eaf0a41f7430b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614936"
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행이 업데이트되었는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>반환 값  
 행이 소유자나 다른 사용자에 의해 시각적으로 업데이트되었고 업데이트가 검색되었으면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 rowUpdated 메서드는 java.sql.ResultSet 인터페이스의 rowUpdated 메서드에 의해 지정 됩니다.  
  
 반환되는 값은 결과 집합에서 업데이트를 검색할 수 있는지 여부에 따라 달라집니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 모든 커서 유형에 대해 업데이트된 행을 검색하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
