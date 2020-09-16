---
description: setNString 메서드(int, java.lang.String)
title: setNString 메서드(int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b7da6d44-f5b1-44f8-95f5-40179968b1b0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2d02b382ae11e8d607689153ee04f56f2bfa95b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458665"
---
# <a name="setnstring-method-int-javalangstring"></a>setNString 메서드(int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 **문자열** 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNString(int parameterIndex,  
                                                  java.lang.String value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
 *value*  
  
 매개 변수 값이 들어 있는 **문자열** 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 데이터 형식에 사용해야 합니다.  
  
 이 setNString 메서드는 java.sql.PreparedStatement 인터페이스의 setNString 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerPreparedStatement 멤버](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
