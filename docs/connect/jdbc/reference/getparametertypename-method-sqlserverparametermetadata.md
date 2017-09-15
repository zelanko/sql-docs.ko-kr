---
title: "getParameterTypeName 메서드 (SQLServerParameterMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerParameterMetaData.getParameterTypeName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ebe7ff0f-3cc0-408e-9503-4ca754c9c37f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 12c0f6363284c729e389586f39c5499303675acb
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getparametertypename-method-sqlserverparametermetadata"></a>getParameterTypeName 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수의 데이터베이스 관련 형식 이름을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getParameterTypeName(int param)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *param*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 형식 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getParameterTypeName 메서드는 java.sql.ParameterMetaData 인터페이스의 getParameterTypeName 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
