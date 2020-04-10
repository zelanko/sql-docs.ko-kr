---
title: prepareStatement 메서드(java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 72b5c4a5-1382-4b2c-80a0-47c97c5f52d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8705df79119f8580d43b813dc1d9d9fcfc8c0ffd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80913950"
---
# <a name="preparestatement-method-javalangstring-int"></a>prepareStatement 메서드(java.lang.String, int[])
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  데이터베이스로 매개 변수가 있는 SQL 문을 보내기 위한 [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 개체를 만들며, 특정 배열로 지정된 자동 생성 키를 검색할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
                                                   int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sql*  
  
 SQL 문이 포함된 **문자열**입니다.  
  
 *columnIndexes*  
  
 정수 배열입니다.  
  
## <a name="return-value"></a>Return Value  
 PreparedStatement 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 prepareStatement 메서드는 java.sql.Connection 인터페이스의 prepareStatement 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [prepareStatement 메서드 &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection 멤버](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 클래스](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
