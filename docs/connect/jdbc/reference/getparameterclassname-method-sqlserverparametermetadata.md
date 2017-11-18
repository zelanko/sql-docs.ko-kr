---
title: "getParameterClassName 메서드 (SQLServerParameterMetaData) | Microsoft Docs"
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
apiname:
- SQLServerParameterMetaData.getParameterClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 545634d8-f06b-429a-9293-0087d758f359
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53d055fe1ddfc16e688c9277fc643d95a282b604
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getparameterclassname-method-sqlserverparametermetadata"></a>getParameterClassName 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  에 해당 인스턴스로 전달 되어야 하는 Java 클래스의 정규화 된 이름을 검색는 [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 의 메서드는 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 클래스입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getParameterClassName(int param)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *param*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **문자열** 정규화 된 클래스 이름이 들어 있는입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getParameterClassName 메서드는 java.sql.ParameterMetaData 인터페이스의 getParameterClassName 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

