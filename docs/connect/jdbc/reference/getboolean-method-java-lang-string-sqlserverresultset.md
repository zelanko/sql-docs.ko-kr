---
description: getBoolean 메서드(java.lang.String)(SQLServerResultSet)
title: getBoolean 메서드(java.lang.String)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBoolean (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ba98a27b-722d-4904-ac65-0f082fde1fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db6e0b69c4135780db0bb55c74de311a1674b438
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437065"
---
# <a name="getboolean-method-javalangstring-sqlserverresultset"></a>getBoolean 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 이름의 값을 Java 프로그래밍 언어의 **boolean**로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean getBoolean(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
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
  
  
