---
title: updateDateTimeOffset(string) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 952947ce-7c6e-4364-b035-46cb7fe621b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef75855c27190a2b79833a75ef991283f23305be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617461"
---
# <a name="updatedatetimeoffsetstring-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(string, microsoft.sql.DateTimeOffset)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 열 이름이 지정된 경우 지정된 열 값을 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름입니다.  
  
 *x*  
  
 A [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 검색할 수 있습니다는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값을 [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateDateTimeOffset&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
