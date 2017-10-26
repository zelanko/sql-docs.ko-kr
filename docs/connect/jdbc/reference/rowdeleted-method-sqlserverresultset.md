---
title: "rowDeleted 메서드 (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f2c4e8e106f749fd087cf47d2c444743ef27172
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="rowdeleted-method-sqlserverresultset"></a>rowDeleted 메서드 (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  행이 삭제되었는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 및 삭제 감지 하 고 행을 삭제 한 경우. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 rowDeleted 메서드는 java.sql.ResultSet 인터페이스의 rowDeleted 메서드에 의해 지정 됩니다.  
  
 삭제된 행은 결과 집합에 가시적인 빈틈을 남겨 둘 수 있습니다. 이 메서드를 사용하면 결과 집합에서 빈틈을 검색할 수 있습니다. 반환 되는 값에 따라 다릅니다.이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체 삭제 내용을 검색할 수 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]검색이 정방향 및 동적 커서에 대해 일시적 이기는 하지만 모든 업데이트 가능 커서 유형에 대해 삭제 된 행을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

