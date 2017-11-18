---
title: "rowUpdated 메서드 (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5f9b34859431b995ddfe6788b6eb08d6d9ed9d74
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행이 업데이트되었는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 모두 행이 소유자나 다른 사용자에 의해 시각적으로 업데이트 된 하 고 업데이트의 검색 합니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 rowUpdated 메서드는 java.sql.ResultSet 인터페이스의 rowUpdated 메서드에 의해 지정 됩니다.  
  
 반환되는 값은 결과 집합에서 업데이트를 검색할 수 있는지 여부에 따라 달라집니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]모든 커서 유형에 대해 업데이트 된 행을 검색 하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

