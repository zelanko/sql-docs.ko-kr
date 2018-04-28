---
title: getNCharacterStream 메서드 (int) (SQLServerResultSet) | Microsoft Docs
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
ms.topic: article
ms.assetid: f1cfa4e4-3e1f-4504-b0de-cc626d653661
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58806731b46a15d07e86d95e970debec621d9b69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="getncharacterstream-method-int-sqlserverresultset"></a>getNCharacterStream 메서드(int)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  현재 행에서 지정 된 열의 값을 검색 하는 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 판독기 개체로 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getNCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 판독기 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getNCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 getNCharacterStream 메서드에 의해 지정 됩니다.  
  
 값을 검색 하려면이 메서드를 사용할 수는 **nvarchar**, **nchar**, **nvarchar (max)**, **ntext**, 또는 **xml** 현재 행의 열 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체입니다. 이 메서드를 사용하여 다른 데이터 형식의 값을 검색하려고 하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNCharacterStream 메서드 &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
