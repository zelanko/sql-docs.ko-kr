---
title: getParameterMode 메서드(SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getParameterMode
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d93c9b70-18c2-44bb-a6de-70a7e940d806
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223be5e4f95c8986f48dedcf907f7df4ad646056
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80904439"
---
# <a name="getparametermode-method-sqlserverparametermetadata"></a>getParameterMode 메서드(SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수의 모드를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getParameterMode(int param)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *param*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 지정된 매개 변수의 모드를 나타내는 **int**로, 다음 값 중 하나에 해당됩니다.  
  
 ParameterMetaData.parameterModeIn  
  
 ParameterMetaData.parameterModeInOut  
  
 ParameterMetaData.parameterModeOut  
  
 ParameterMetaData.parameterModeUnknown  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getParameterMode 메서드는 java.sql.ParameterMetaData 인터페이스의 getParameterMode 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerParameterMetaData 메서드](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [SQLServerParameterMetaData 멤버](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [SQLServerParameterMetaData 클래스](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
