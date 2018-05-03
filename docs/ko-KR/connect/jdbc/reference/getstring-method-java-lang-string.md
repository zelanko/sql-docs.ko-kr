---
title: getString 메서드 (java.lang.String) | Microsoft Docs
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
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fba79381d9a60dde16734c31e332cb096fde7216
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getstring-method-javalangstring"></a>getString 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  로 지정된 된 매개 변수의 값을 검색 하는 **문자열** java 프로그래밍 언어 매개 변수 이름이 지정 됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getString 메서드는 java.sql.CallableStatement 인터페이스의 getString 메서드에 의해 지정 됩니다.  
  
 모든 열 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] string으로 반환 될 수 있습니다. 즉, 모든 숫자 기반 및 문자 기반 형식의 문자열 표현과 binary, varbinary, varbinary(max), image, timestamp 및 uniqueidentifier 같은 이진 열의 16진수 문자 표현이 반환될 수 있습니다.  
  
 money, smallmoney, datetime, smalldatetime, float, real, decimal 및 numeric과 같이 위치에 영향을 받는 형식은 해당 형식의 기본 값에 대해 정규 toString() 형식을 반환합니다.  
  
 사용자 정의 형식은 16진수 문자열 값으로 반환됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getString 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
