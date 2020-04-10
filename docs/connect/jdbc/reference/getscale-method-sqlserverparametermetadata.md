---
title: getScale 메서드(SQLServerParameterMetaData) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e55fe6d5407cb9ab46f57e125f34d4e14dcdb9d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921754"
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
  
## <a name="return-value"></a>Return Value  
 지정된 매개 변수의 소수 자릿수를 나타내는 **int**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getScale 메서드는 java.sql.ParameterMetaData 인터페이스의 getScale 메서드에 의해 지정됩니다.  
  
 이 메서드는 열의 소수점 이하 자릿수를 가져옵니다. 소수점이 없는 형식의 경우 이 메서드는 "0"을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
