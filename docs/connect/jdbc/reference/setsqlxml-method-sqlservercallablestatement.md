---
title: setSQLXML 메서드(SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: de095cb3-1111-4154-8996-3c2e529e3000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82e8d1507760591b4e019d5d785eb0cc6a93c3ac
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924921"
---
# <a name="setsqlxml-method-sqlservercallablestatement"></a>setSQLXML 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 SQLXML 개체로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final void setSQLXML(java.lang.String parameterName,  
                            java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름을 나타내는 **String**입니다.  
  
 *xmlObject*  
  
 매개 변수 값이 들어 있는 SQLXML 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setSQLXML 메서드는 java.sql.CallableStatement 인터페이스의 setSQLXML 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
