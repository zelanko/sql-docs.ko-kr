---
title: getNClob 메서드(java.lang.String)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36571f7c-b335-4249-8f83-51dcb6923aec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a7241be8ab1c8ffcaf6b4eb143740f3ca09161d
ms.sourcegitcommit: ef15fa253d98c62538bf9b6fe191af7f8ef8f6c8
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49991136"
---
# <a name="getnclob-method-javalangstring-sqlserverresultset"></a>getNClob 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열의 값을 Java 프로그래밍 언어의 NClob 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.NClob getNClob(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블이 포함된 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 NClob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getNClob 메서드는 java.sql.ResultSet 인터페이스의 getNClob 메서드에 의해 지정됩니다.  
  
 이 메서드는 에서만 지원 됩니다 **nvarchar (max)** 하십시오 **ntext**, 및 **xml** 열입니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNClob 메서드(SQLServerResultSet)](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
