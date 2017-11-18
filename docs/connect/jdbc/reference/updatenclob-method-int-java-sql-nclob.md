---
title: "updateNClob 메서드 (int, java.sql.NClob) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6e9bca18-f64e-46a4-8541-2c9c39b393b5
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e517dd13a458274a2784fb4ff68c85a7544a8f8e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updatenclob-method-int-javasqlnclob"></a>updateNClob 메서드(int, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  으로 지정된 된 열 업데이트는 **NClob** 값입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateNClob(int columnIndex,  
                        java.sql.NClob nClob)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
 *nClob*  
  
 NClob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 updateNClob 메서드는 java.sql.ResultSet 인터페이스의 updateNClob 메서드에 의해 지정 됩니다.  
  
 이 메서드는의 경우에 지원 **nvarchar (max)**, **ntext**, 및 **xml** 열입니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [updateNClob 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

