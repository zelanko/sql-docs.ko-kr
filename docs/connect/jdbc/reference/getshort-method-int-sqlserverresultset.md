---
title: "getShort 메서드 (int) (SQLServerResultSet) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.getShort (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0b543c92-feb8-46a4-8477-9b5f94f1cdc7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c242920d35d4360beac4f03f8430d06627646835
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="getshort-method-int-sqlserverresultset"></a>getShort 메서드 (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 현재 행에서 지정 된 열 인덱스의 값을 검색 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체로 **짧은** Java 프로그래밍 언어의에서 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public short getShort(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 **int** 열 인덱스를 나타내는입니다.  
  
## <a name="return-value"></a>반환 값  
 A **짧은** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>주의  
 이 getShort 메서드는 java.sql.ResultSet 인터페이스의 getShort 메서드에 의해 지정 됩니다.  
  
 이 메서드는 에서만 지원 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] smallint, tinyint 및 bit와 같이 정수 값을 안전 하 게 반환할 수 있는 데이터 형식입니다. 다른 데이터 형식에 이 메서드를 사용하면 예외가 발생합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [getShort 메서드 &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
