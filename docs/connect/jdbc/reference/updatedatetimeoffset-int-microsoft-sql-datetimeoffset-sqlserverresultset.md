---
title: updateDateTimeOffset(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21ec0054-c808-4e88-9c8d-c71b696ce658
author: MightyPen
ms.author: genemi
ms.openlocfilehash: caad3533d06ad7c00a4fb2cd8000bdd12c51acdc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67999113"
---
# <a name="updatedatetimeoffsetint-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(int, microsoft.sql.DateTimeOffset)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 열 서수(0부터 시작)가 지정된 경우 지정된 열 값을 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 열 서수(0부터 시작)입니다.  
  
 *x*  
  
 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)을 사용하여 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 값을 검색할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateDateTimeOffset&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
