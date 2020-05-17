---
title: getDateTimeOffset 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8bb00356-4d6e-4625-b924-67646930fdf2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec297d1b01b6d7cf8d292d2f4518aa5b51cd9704
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67983834"
---
# <a name="getdatetimeoffset-method-int"></a>getDateTimeOffset 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 메서드는 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 매개 변수 인덱스가 지정된 경우 지정된 매개 변수의 값을 Java 프로그래밍 언어의 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int index)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 매개 변수 서수(1부터 시작)입니다.  
  
## <a name="return-value"></a>Return Value  
 [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 [SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md)을 사용하여 [DateTimeOffset Class](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md) 매개 변수 값을 설정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [getDateTimeOffset 메서드&#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
