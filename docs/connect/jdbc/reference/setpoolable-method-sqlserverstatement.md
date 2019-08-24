---
title: setPoolable 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5424de7d0d6f7bda44ec61ea61f48d63bb097c97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973203"
---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문을 풀링하거나 풀링하지 않도록 요청합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>매개 변수  
 *poolable*  
  
 **true**이면 문을 풀링하도록 요청하고, **false**이면 문을 풀링하지 않도록 요청합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 *poolable* 매개 변수에 지정된 값은 문 풀 구현 시 애플리케이션에서 문을 풀링하기를 원하는지 여부를 나타내는 힌트로 사용됩니다. 이 힌트를 사용할지 여부는 문 풀 관리자가 결정합니다.  
  
 문의 풀 값은 드라이버에 의해 구현된 내부 문 캐시와 애플리케이션 서버 및 다른 애플리케이션에 의해 구현된 외부 문 캐시 모두에 적용됩니다.  
  
 기본적으로 SQLServerStatement 개체는 생성 시 poolable 되지 않습니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 개체는 생성 될 때 poolable 됩니다.  
  
 닫힌 문에 대해 이 메서드를 호출하면 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)이 발생합니다.  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)은 개체가 풀링 가능한지 여부를 나타내는 값을 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
