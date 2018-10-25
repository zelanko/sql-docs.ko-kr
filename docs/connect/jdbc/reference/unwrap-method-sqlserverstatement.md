---
title: unwrap 메서드(SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce680176-ef04-4e44-bb6c-ec50bd06e7e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a6823a9f6f57e1ebf1348f35d4a1478100962bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785557"
---
# <a name="unwrap-method-sqlserverstatement"></a>unwrap 메서드(SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드에 액세스할 수 있도록 지정된 인터페이스를 구현하는 개체를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 인터페이스를 정의하는 **T** 형식의 클래스입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 인터페이스를 구현하는 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) 메서드는 JDBC 4.0 사양에서 도입된 java.sql.Wrapper 인터페이스에 의해 정의됩니다.  
  
 응용 프로그램에서는 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]와 관련된 JDBC API에 대한 확장에 액세스해야 할 수 있습니다. unwrap 메서드는 이 개체가 확장하는 공용 클래스에서 공급업체 확장을 노출하는 경우 이 클래스에 대한 래핑 해제를 지원합니다.  
  
 이 메서드가 호출되면 개체가 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 클래스로 래핑 해제됩니다.  
  
 예제 코드를 참조 하세요 [큰 데이터 업데이트 샘플](../../../connect/jdbc/updating-large-data-sample.md), 또는 [unwrap 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [isWrapperFor 메서드 &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)   
 [SQLServerStatement 멤버](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
