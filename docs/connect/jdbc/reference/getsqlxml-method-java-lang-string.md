---
description: getSQLXML 메서드(java.lang.String)
title: getSQLXML 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f56b192a-3255-4215-b552-8e494fbca083
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 923fbcdbbc1624a3a196ef1dedb4619251f58ad4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434455"
---
# <a name="getsqlxml-method-javalangstring"></a>getSQLXML 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 검색하여 SQLXML 개체로 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.sql.SQLXML getSQLXML(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름을 나타내는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 ASQLXMLobject입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getSQLXML 메서드는 java.sql.CallableStatement 인터페이스의 getSQLXML 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getSQLXML 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
