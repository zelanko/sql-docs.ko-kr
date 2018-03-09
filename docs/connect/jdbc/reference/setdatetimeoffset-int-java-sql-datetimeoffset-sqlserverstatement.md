---
title: setDateTimeOffset (int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9b18af7823f8d02f80ba636fe57b5d6cd807770
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset)(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 DateTimeOffset 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 설정할 열의 인덱스입니다.  
  
 *dateTimeOffset*  
  
 DateTimeOffset 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 DateTimeOffset 형식은 "YYYY-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM"입니다. 다음 표를 참조하십시오.  
  
|SQL 형식|Insert|  
|--------------|------------|  
|datetime|"YYYY-MM-DD hh:mm:ss[.nnn]"만 삽입 가능|  
|smalldatetime|"YYYY-MM-DD hh:mm:ss"만 삽입 가능|  
|Time|"hh:mm:ss[.nnnnnnn]"만 삽입 가능|  
|날짜|"YYYY-MM-DD"만 삽입 가능|  
|datetime2|"YYYY-MM-DD hh:mm:ss[.nnnnnnn]"만 삽입 가능|  
  
## <a name="see-also"></a>관련 항목:  
 [getDateTimeOffset &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
