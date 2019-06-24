---
title: getNString 메서드 (int) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 03a11c4479ac860e84009fcd528d932098bdc661
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66784344"
---
# <a name="getnstring-method-int"></a>getNString 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 값을 검색 **NCHAR**를 **NVARCHAR**, 또는 **LONGNVARCHAR** 문자열로 java에서 프로그래밍 언어 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getNString(int parameterIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 AStringobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getNString 메서드는 java.sql.CallableStatement 인터페이스의 getNString 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNString 메서드(SQLServerCallableStatement)](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
