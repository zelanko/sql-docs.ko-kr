---
title: getAsciiStream 메서드 (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getAsciiStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1ec7e246-4b91-4420-9a4c-0ebd98e2e38b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a96c4e91c449c6055d960fee13f429867ffddd0c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47643019"
---
# <a name="getasciistream-method-int"></a>getAsciiStream 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 ASCII 문자의 스트림으로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.InputStream getAsciiStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 InputStream 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 getAsciiStream 메서드는 java.sql.ResultSet 인터페이스의 getAsciiStream 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getAsciiStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
