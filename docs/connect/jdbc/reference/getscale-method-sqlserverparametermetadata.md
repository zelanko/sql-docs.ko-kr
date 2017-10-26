---
title: "getScale 메서드 (SQLServerParameterMetaData) | Microsoft Docs"
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
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be05360747e2b67de20d6e93823b77629b5bbbac
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getscale-method-sqlserverparametermetadata"></a>getScale 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수의 소수점 이하 자릿수를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *param*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 **int** 지정된 된 매개 변수의 소수 자릿수를 나타내는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getScale 메서드는 java.sql.ParameterMetaData 인터페이스의 getScale 메서드에 의해 지정 됩니다.  
  
 이 메서드는 열의 소수점 이하 자릿수를 가져옵니다. 소수점이 없는 형식의 경우 이 메서드는 "0"을 반환합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

