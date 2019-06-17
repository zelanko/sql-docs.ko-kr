---
title: getdatetimeoffset (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 60abf83d-6f97-4e47-b9d3-5072bd09d869
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 37bd84db5e5aeb4355234d126c4356b73a5ec6d3
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777151"
---
# <a name="getdatetimeoffsetint-sqlserverresultset"></a>getDateTimeOffset(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 매개 변수 인덱스가 지정된 경우 지정된 열의 값을 Java 프로그래밍 언어의 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 서수입니다.  
  
## <a name="return-value"></a>반환 값  
 A [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 업데이트할 수는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값을 [sqlserverresultset.updatedatetimeoffset을](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
