---
title: getSQLXML 메서드 (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab9c7b10-026f-4a51-8d60-e6871d1abd02
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8062f6c5748155d6d1a3a598febc3f70344fe5a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32838798"
---
# <a name="getsqlxml-method-javalangstring-sqlserverresultset"></a>getSQLXML 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) SQLXML 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 A **문자열** 열 레이블을 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 ASQLXMLobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getSQLXML 메서드는 java.sql.ResultSet 인터페이스의 getSQLXML 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getSQLXML 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
