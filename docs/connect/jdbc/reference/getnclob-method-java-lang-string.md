---
title: "getNClob 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b15e1e45adb9960c42f917647e66bd4785e4cad8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getnclob-method-javalangstring"></a>getNClob 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC의 값을 검색 **NCLOB** 를 Java 프로그래밍 언어에에서 NClob 개체와 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 ANClobobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getNClob 메서드는 java.sql.CallableStatement 인터페이스의 getNClob 메서드에 의해 지정 됩니다.  
  
 이 메서드 검색 지원 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 매개 변수입니다. 다른 데이터 형식 매개 변수에서 이러한 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNClob 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
