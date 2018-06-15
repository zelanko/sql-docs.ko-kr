---
title: getTime 메서드 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e18c84f5-7171-4057-8c9e-fe1d43ae9c20
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e5d86e6ad808d69b64e5dd9abed03cf5513cf5c2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838438"
---
# <a name="gettime-method-int-sqlserverresultset"></a>getTime 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) Java 프로그래밍 언어의에서 java.sql.Time 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 시간 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getTime 메서드는 java.sql.ResultSet 인터페이스의 getTime 메서드에 의해 지정 됩니다.  
  
 유효한 시간 부분을 반환 하는이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] datetime 또는 smalldatetime 데이터 형식의 날짜 부분은 Java 기준 날짜인 1970-01-01로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getTime 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
