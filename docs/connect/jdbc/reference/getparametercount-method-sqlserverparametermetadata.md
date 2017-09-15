---
title: "getParameterCount 메서드 (SQLServerParameterMetaData) | Microsoft Docs"
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
- SQLServerParameterMetaData.getParameterCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7dbbdacb-74ef-42e7-9bdc-a3229505dad8
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5928f7a848a887078f102b010f3e92d6d900f231
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getparametercount-method-sqlserverparametermetadata"></a>getParameterCount 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 수를 검색 된 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 이 대 한 개체 [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 개체 정보를 포함 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getParameterCount()  
```  
  
## <a name="return-value"></a>반환 값  
 **int** 매개 변수 개수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getParameterCount 메서드는 java.sql.ParameterMetaData 인터페이스의 getParameterCount 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
