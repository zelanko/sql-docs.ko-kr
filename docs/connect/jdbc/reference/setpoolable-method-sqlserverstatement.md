---
title: "setPoolable 메서드 (SQLServerStatement) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 674f138128dcfda2dc4b924e3b04f148d42b69c5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable 메서드 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  문을 풀링하거나 풀링하지 않도록 요청합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>매개 변수  
 *풀링*  
  
 경우 **true**, 문을 풀링 하도록 요청 합니다. 경우 **false**, 문을 풀링 하지을 요청 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 에 지정 된 값의 *풀링* 매개 변수는 응용 프로그램에서 문을 풀링 하기를 전달할지 여부를 나타내는 문 풀 구현에 대 한 힌트입니다. 이 힌트를 사용할지 여부는 문 풀 관리자가 결정합니다.  
  
 문의 풀 값은 드라이버에 의해 구현된 내부 문 캐시와 응용 프로그램 서버 및 다른 응용 프로그램에 의해 구현된 외부 문 캐시 모두에 적용됩니다.  
  
 기본적으로 SQLServerStatement 개체는 풀링 가능한 상태로 만들어집니다. SQLServerPreparedStatement 및 SQLServerCallableStatement 개체는 풀링 가능한 상태로 만들어집니다.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) 닫힌된 문에 대해이 메서드를 호출 하면 throw 됩니다.  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md) 개체 풀링 인지 여부를 나타내는 값을 반환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

