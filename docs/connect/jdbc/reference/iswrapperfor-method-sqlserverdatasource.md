---
title: isWrapperFor 메서드(SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f77af027-c021-4a17-b264-1ee592bfdd84
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cf4f7df354f8aa821305e7e847a060491e0e5a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631381"
---
# <a name="iswrapperfor-method-sqlserverdatasource"></a>isWrapperFor 메서드(SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터 원본 개체가 지정된 인터페이스에 대한 래퍼인지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *iface*  
  
 A **클래스** 인터페이스를 정의 합니다.  
  
## <a name="return-value"></a>반환 값  
 이 개체가 인터페이스를 구현하거나 인터페이스를 구현하는 개체를 래핑하면 **true**이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md) 메서드와 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) 메서드는 JDBC 4.0 사양에서 도입된 java.sql.Wrapper 인터페이스에 의해 정의됩니다.  
  
 이 메서드가 true를 반환하는 경우 동일한 인수로 [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)을 호출하면 성공합니다.  
  
 자세한 내용은 [래퍼 및 인터페이스](../../../connect/jdbc/wrappers-and-interfaces.md)합니다.  
  
## <a name="see-also"></a>참고 항목  
 [unwrap 메서드 &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)   
 [SQLServerDataSource 멤버](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 클래스](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
