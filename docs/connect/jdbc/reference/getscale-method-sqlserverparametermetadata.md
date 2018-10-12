---
title: getScale 메서드 (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3de84426a1c15f45cebe5438e1ac877f32dc154e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718031"
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
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 매개 변수의 소수 자릿수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getScale 메서드는 java.sql.ParameterMetaData 인터페이스의 getScale 메서드에 의해 지정 됩니다.  
  
 이 메서드는 열의 소수점 이하 자릿수를 가져옵니다. 소수점이 없는 형식의 경우 이 메서드는 "0"을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
