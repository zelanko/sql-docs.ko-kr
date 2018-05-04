---
title: getDateTimeOffset 메서드 (String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fedb1d75-0c3d-4eb3-ae65-da0e153265cc
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b49a2459b17a471f3326f0d8a63553467438bcd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="getdatetimeoffset-method-string"></a>getDateTimeOffset 메서드(String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는에서 추가 된 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] JDBC 드라이버 3.0.  
  
 로 지정된 된 매개 변수의 값을 검색 하는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) java 프로그래밍 언어 매개 변수 인덱스가 지정 된 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 A [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 설정할 수 있습니다는 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 매개 변수 값을 [sqlservercallablestatement.setdatetimeoffset을 사용](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getDateTimeOffset 메서드 &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
