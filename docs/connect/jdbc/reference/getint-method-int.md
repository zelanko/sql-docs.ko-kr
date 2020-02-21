---
title: getInt 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getInt (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c86792bb-096e-4c58-8b9e-74491ccf83a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13d8d89a950f57b29c235d823424357dfa8f7bb8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982752"
---
# <a name="getint-method-int"></a>getInt 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 **int**로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public int getInt(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 **int** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getInt 메서드는 java.sql.CallableStatement 인터페이스의 getInt 메서드에 의해 지정됩니다.  
  
 이 메서드는 int, smallint, tinyint 및 bit와 같이 정수 값을 안전하게 반환할 수 있는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식에서만 지원됩니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getInt 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getint-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
