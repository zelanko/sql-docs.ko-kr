---
title: setURL 메서드(SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: de095cb3-1111-4154-8996-3c2e529e3000
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3852a1251bb1f7567276529c1f15f5863ea69731
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800931"
---
# <a name="setsqlxml-method-sqlservercallablestatement"></a>setSQLXML 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된  개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setSQLXML(java.lang.String parameterName,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름을 나타내는 입니다.  
  
 *xmlObject*  
  
 매개 변수 값이 들어 있는  개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setURL 메서드는 java.sql.CallableStatement 인터페이스의 setURL 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
