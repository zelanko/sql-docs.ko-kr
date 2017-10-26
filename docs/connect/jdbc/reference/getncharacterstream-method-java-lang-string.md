---
title: "getNCharacterStream 메서드 (java.lang.String) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 58012af7ac3fe73f07cefc7a65fc97f89a858dc0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  매개 변수 이름이 지정 된 판독기 개체와 지정된 된 매개 변수의 값을 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnLabel*  
  
 A **문자열** 열 레이블이 들어 있는입니다.  
  
## <a name="return-value"></a>반환 값  
 AReaderobject 합니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 에 액세스할 때이 메서드를 사용 해야 **NCHAR**, **NVARCHAR** 및 **LONGNVARCHAR** 매개 변수입니다.  
  
 이 getNCharacterStream 메서드는 java.sql.CallableStatement 인터페이스의 getNCharacterStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getNCharacterStream 메서드 &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  

