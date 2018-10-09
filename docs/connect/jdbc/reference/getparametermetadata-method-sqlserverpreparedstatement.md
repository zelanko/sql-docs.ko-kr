---
title: getParameterMetaData 메서드(SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.getParameterMetaData
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c2876dec-ce29-4b61-9d74-ec3173b8cba5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00a8ad847bdf2f8e36198d79ab89346ac5e8f408
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47787031"
---
# <a name="getparametermetadata-method-sqlserverpreparedstatement"></a>getParameterMetaData 메서드(SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체에 대한 매개 변수의 수, 형식 및 속성을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.ParameterMetaData getParameterMetaData()  
```  
  
## <a name="return-value"></a>반환 값  
 [SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getParameterMetaData 메서드는 java.sql.PreparedStatement 인터페이스의 getParameterMetaData 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement 클래스](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
