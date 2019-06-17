---
title: getURL 메서드 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getURL Ijnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 75d03ced-3614-4997-9abd-24642b1d1aae
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d1ad967d9f3923b886e3713829830be39412620e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769681"
---
# <a name="geturl-method-int"></a>getURL 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 URL 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.net.URL getURL(int n)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *n*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 URL 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getURL 메서드는 java.sql.CallableStatement 인터페이스의 getURL 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getURL 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/geturl-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
