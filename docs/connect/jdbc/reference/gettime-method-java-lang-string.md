---
description: getTime 메서드(java.lang.String)
title: getTime 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ca0a3b29-30d1-4d20-bc8d-d3d9ed19ff50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b4bdcc5eeab3edf282619aac90d6b8bd50fbd81
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434185"
---
# <a name="gettime-method-javalangstring"></a>getTime 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Time 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Time getTime(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 Time 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getTime 메서드는 java.sql.CallableStatement 인터페이스의 getTime 메서드에 의해 지정됩니다.  
  
 이 메서드를 사용하여 검색할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식을 보려면 [데이터 형식 변환 이해](../../../connect/jdbc/understanding-data-type-conversions.md)의 “Getter 메서드 변환”이라는 차트를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [getTime 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
