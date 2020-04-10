---
title: getLong 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getLong (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 92e30537-5fd9-4b67-8b0f-486c6e840e03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd37233f280cd70f7af4742cf5647eb23e74b710
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921322"
---
# <a name="getlong-method-javalangstring"></a>getLong 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 **long**으로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public long getLong(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>Return Value  
 **long** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getLong 메서드는 java.sql.CallableStatement 인터페이스의 getLong 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]bigint **,** int **,** smallint **,** tinyint**및**bit**와 같이 정수 값을 안전하게 반환할 수 있는**  데이터 형식에서만 지원됩니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getLong 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getlong-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
