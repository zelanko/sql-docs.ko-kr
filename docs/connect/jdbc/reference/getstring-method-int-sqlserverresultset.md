---
title: getString 메서드 (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae964d0005650c36b93b4c186765f652016f28ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getstring-method-int-sqlserverresultset"></a>getString 메서드 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **문자열** Java 프로그래밍 언어의에서 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getString 메서드는 java.sql.ResultSet 인터페이스의 getString 메서드에 의해 지정 됩니다.  
  
 모든 열 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] String으로 반환 될 수 있습니다. 즉, 한 **문자열** 모든 숫자 기반 및 문자 기반 형식 표현과 binary, varbinary, varbinary (max), 이미지, 타임 스탬프 및 uniqueidentifier 같은 이진 열의 16 진수 문자열 표현 될 수 있습니다 반환 됩니다.  
  
 money, smallmoney, datetime, smalldatetime, float, real, decimal 및 numeric과 같이 위치에 영향을 받는 형식은 해당 형식의 기본 값에 대해 정규 toString() 형식을 반환합니다.  
  
 사용자 정의 형식은 16 진수로 반환 됩니다 **문자열** 값입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getString 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
