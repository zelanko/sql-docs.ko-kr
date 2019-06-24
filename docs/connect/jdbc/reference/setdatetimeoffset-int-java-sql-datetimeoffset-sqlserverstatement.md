---
title: setDateTimeOffset(int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 36b23fb46e8cd909cf71e696293f2981731a86d2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66793923"
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
  
## <a name="remarks"></a>Remarks  
 DateTimeOffset 형식은 "YYYY-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM"입니다. 다음 표를 참조하십시오.  
  
|SQL 형식|Insert|  
|--------------|------------|  
|DATETIME|"YYYY-MM-DD hh:mm:ss[.nnn]"만 삽입 가능|  
|smalldatetime|"YYYY-MM-DD hh:mm:ss"만 삽입 가능|  
|Time|"hh:mm:ss[.nnnnnnn]"만 삽입 가능|  
|date|"YYYY-MM-DD"만 삽입 가능|  
|datetime2|"YYYY-MM-DD hh:mm:ss[.nnnnnnn]"만 삽입 가능|  
  
## <a name="see-also"></a>참고 항목  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
