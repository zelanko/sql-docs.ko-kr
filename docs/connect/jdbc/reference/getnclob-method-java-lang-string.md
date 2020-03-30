---
title: getNClob 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be01ce56-8f13-437b-8de6-246cda5f7830
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbe655691ed898dfbb8eac5da5bb28d4d6cde686
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981499"
---
# <a name="getnclob-method-javalangstring"></a>getNClob 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC **NCLOB** 매개 변수의 값을 Java 프로그래밍 언어의 NClob 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.NClob getNClob(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 NClob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getNClob 메서드는 java.sql.CallableStatement 인터페이스의 getNClob 메서드에 의해 지정됩니다.  
  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT** 및 **XML** 매개 변수 검색만 지원합니다. 다른 데이터 형식 매개 변수에서 이러한 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNClob 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
