---
title: getNClob 메서드 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 10dfa251-9408-469e-ae2a-1acf3917cf47
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f86551744ac69ef5dc6f63446689d535cad620cb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getnclob-method-int"></a>getNClob 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정 된 JDBC의 값을 검색 **NCLOB** 를 Java 프로그래밍 언어에에서 NClob 개체와 매개 변수입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.NClob getNClob(int parameterIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterIndex*  
  
 **int** 매개 변수 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 ANClobobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getNClob 메서드는 java.sql.CallableStatement 인터페이스의 getNClob 메서드에 의해 지정 됩니다.  
  
 이 메서드 검색 지원 **NCHAR**, **NVARCHAR**, **NTEXT**, 및 **XML** 매개 변수입니다. 다른 데이터 형식 매개 변수에서 이러한 메서드를 호출하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNClob 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
