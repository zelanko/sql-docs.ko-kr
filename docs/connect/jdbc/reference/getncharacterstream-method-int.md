---
title: getNCharacterStream 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6ae704f5-823c-4dfe-8c08-07b547c61a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ed91df645edd7083e0d91346dfdf6d39bebd91d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67981653"
---
# <a name="getncharacterstream-method-int"></a>getNCharacterStream 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Reader 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.io.Reader getNCharacterStream(int parameterIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 매개 변수 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>Return Value  
 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 메서드는 **NCHAR**, **NVARCHAR** 및 **LONGNVARCHAR** 매개 변수에 액세스할 때 사용해야 합니다.  
  
 이 getNCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 getNCharacterStream 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNCharacterStream 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
