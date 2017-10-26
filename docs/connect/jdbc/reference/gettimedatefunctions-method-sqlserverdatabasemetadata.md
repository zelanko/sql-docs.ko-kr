---
title: "getTimeDateFunctions 메서드 (SQLServerDatabaseMetaData) | Microsoft Docs"
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
- SQLServerDatabaseMetaData.getTimeDateFunctions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a56e08ae-6f4e-4dc6-b175-ff457d0d7a81
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d26d4a2adf59b27b9c8146799902074cbcfb7e2
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="gettimedatefunctions-method-sqlserverdatabasemetadata"></a>getTimeDateFunctions 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스와 함께 사용할 수 있는 시간 및 날짜 함수의 쉼표로 구분된 목록을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getTimeDateFunctions()  
```  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 시간 및 날짜 함수의 목록이 들어 있습니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTimeDateFunctions 메서드는 java.sql.DatabaseMetaData 인터페이스의 getTimeDateFunctions 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

