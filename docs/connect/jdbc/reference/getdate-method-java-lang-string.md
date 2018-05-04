---
title: getDate 메서드 (java.lang.String) 매개 변수 | Microsoft Docs
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
- SQLServerCallableStatement.getDate (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a605bca6-d960-4756-ad14-0f42b313e60a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 004e82182e71cb1f37f466cc89e86eb0a0399ba9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getdate-method-javalangstring"></a>getDate 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 Java 프로그래밍 언어의 java.sql.Date 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 Date 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getDate 메서드는 java.sql.CallableStatement 인터페이스의 getDate 메서드에 의해 지정 됩니다.  
  
 유효한 날짜 부분을 반환 하는이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** 또는 **smalldatetime** 데이터 형식의 시간 부분은 Java 기준 시간인 00:00 (자정)으로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getDate 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
