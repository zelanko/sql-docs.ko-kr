---
title: "getNCharacterStream 메서드 (java.lang.String) (SQLServerResultSet) | Microsoft Docs"
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
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9219eb9e9d5b7d4a0aecf00049beba4b450fa029
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>getNCharacterStream 메서드(java.lang.String)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 판독기 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 열 레이블을 포함 하는 문자열입니다.  
  
## <a name="return-value"></a>반환 값  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 getNCharacterStream 메서드에 의해 지정 됩니다.  
  
 값을 검색 하려면이 메서드를 사용할 수는 **nvarchar**, **nchar**, **nvarchar (max)**, **ntext**, 또는 **xml** 현재 행의 열 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다. 이 메서드를 사용하여 다른 데이터 형식의 값을 검색하려고 하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNCharacterStream 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
