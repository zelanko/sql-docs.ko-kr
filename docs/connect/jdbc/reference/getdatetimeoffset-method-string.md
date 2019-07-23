---
title: getDateTimeOffset 메서드 (String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fedb1d75-0c3d-4eb3-ae65-da0e153265cc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d831ff519f72fb5b68cec3c7dc359f1d54106c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983785"
---
# <a name="getdatetimeoffset-method-string"></a>getDateTimeOffset 메서드(String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String sCol)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 [DateTimeOffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [SQLServerCallableStatement](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md)를 사용 하 여 [datetimeoffset 클래스](../../../connect/jdbc/reference/datetimeoffset-class.md) 매개 변수 값을 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getDateTimeOffset 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
