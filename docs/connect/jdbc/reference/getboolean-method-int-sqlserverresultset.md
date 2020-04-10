---
title: getBoolean 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBoolean (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 50fcc0c3-36a1-47b2-b18c-7aa2ac9b27d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a49581f943e369e43a77cdb7a44375dd4489465
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926372"
---
# <a name="getboolean-method-int-sqlserverresultset"></a>getBoolean 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 Java 프로그래밍 언어의 **boolean**으로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getBoolean(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 **부울** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getBoolean 메서드는 java.sql.ResultSet 인터페이스의 getBoolean 메서드에 의해 지정됩니다.  
  
 이 메서드는 숫자 및 문자 데이터 형식에서만 지원됩니다. “1”, 1 및 “**true**” 값을 **true**로 변환하고, “0”, 0 및 “**false**” 값을 **false**로 변환합니다. 다른 모든 값에 대한 동작은 정의되어 있지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getBoolean 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
