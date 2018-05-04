---
title: getDateTimeOffset(java.lang.string) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e585927c-0dee-43fd-b71e-c9f1701790bd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c85793304acfbd8ffe8ce115dd95b7ad84085fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getdatetimeoffsetjavalangstring-sqlserverresultset"></a>getDateTimeOffset(java.lang.string)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 지정 된 열의 값을 검색 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) java 프로그래밍 언어 매개 변수 인덱스가 지정 된 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 A [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 업데이트할 수 있습니다는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 값과 [sqlserverresultset.updatedatetimeoffset을 사용](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
