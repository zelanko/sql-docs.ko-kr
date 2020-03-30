---
title: getNString 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2048bb9f-7d9b-4aaa-b135-c716910cc800
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbe3bc040ba79ad7699a571b13b48f2c41965c60
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67981424"
---
# <a name="getnstring-method-int"></a>getNString 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Java 프로그래밍 언어인 문자열로 지정된 **NCHAR**, **NVARCHAR** 또는 **LONGNVARCHAR** 매개 변수 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getNString(int parameterIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 String 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getNString 메서드는 java.sql.CallableStatement 인터페이스의 getNString 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNString 메서드(SQLServerCallableStatement)](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
