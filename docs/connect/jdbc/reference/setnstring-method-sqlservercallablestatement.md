---
title: "setNString 메서드 (SQLServerCallableStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6494300b-7fc0-4076-8311-22d35a96cdc6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7748fe8a19028542d76cda580f6bbb7c24f3a7a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setnstring-method-sqlservercallablestatement"></a>setNString 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 된 String 개체를 지정된 된 매개 변수를 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNString(java.lang.String parameterName, java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 A **문자열** 매개 변수 이름을 나타내는입니다.  
  
 *value*  
  
 String 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 에 대 한이 메서드를 사용 해야 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 데이터 형식입니다.  
  
 이 setNString 메서드는 java.sql.CallableStatement 인터페이스의 setNString 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

