---
description: setNClob 메서드(java.lang.String, java.sql.NClob)
title: setNClob 메서드(java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bf119306e3c937a8998670d7f22611e0b9772b6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88458695"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>setNClob 메서드(java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 NClob 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *value*  
  
 NClob 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 메서드는 **NCHAR**, **NVARCHAR**, **NTEXT**및 **XML** 매개 변수 데이터 형식에 사용해야 합니다.  
  
 이 setNClob 메서드는 java.sql.CallableStatement 인터페이스의 setNClob 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNClob 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
