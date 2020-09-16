---
description: getFloat 메서드(int)(SQLServerResultSet)
title: getFloat 메서드(int)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getFloat (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 30863ef5-7a7c-440e-8fbb-426a99266ee1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd05df07b3be9da295bd39aae57dd15a2ff63d17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436005"
---
# <a name="getfloat-method-int-sqlserverresultset"></a>getFloat 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 Java 프로그래밍 언어의 **float**로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public float getFloat(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 **float** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getFloat 메서드는 java.sql.ResultSet 인터페이스의 getFloat 메서드에 의해 지정됩니다.  
  
 이 메서드는 Java **float** 정확성이 유지되는 모든 숫자 기반 형식을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getFloat 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
