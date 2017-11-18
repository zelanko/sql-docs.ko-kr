---
title: "setDateTimeOffset 메서드 (SQLServerPreparedStatement) | Microsoft Docs"
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
ms.assetid: 5014dba9-1755-4769-b070-6cbeecee864e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e043ac3d0d38bc985fa05909f07ff32a7d63810a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setdatetimeoffset-method-sqlserverpreparedstatement"></a>setDateTimeOffset 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 에 지정 된 열의 값을 설정 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setDateTimeOffset(int n, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 열 서수(0부터 시작)입니다.  
  
 *x*  
  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

