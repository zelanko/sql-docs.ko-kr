---
title: getDate 메서드(int, java.util.Calendar)(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getDate (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 150411f7-2a73-4380-b921-9698acd5d1f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8dd9e6920aadec8434bfe7629cad9e1c8a22215d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922733"
---
# <a name="getdate-method-int-javautilcalendar-sqlserverresultset"></a>getDate 메서드(int, java.util.Calendar)(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 지정된 Calendar 개체를 사용하여 Java 프로그래밍 언어의 java.sql.Date 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.sql.Date getDate(int columnIndex,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *cal*  
  
 Calendar 개체입니다.  
  
## <a name="return-value"></a>Return Value  
 Date 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getDate 메서드는 java.sql.ResultSet 인터페이스의 getDate 메서드에 의해 지정됩니다.  
  
 이 메서드는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] datetime 또는 smalldatetime 데이터 형식의 유효한 날짜 부분을 반환합니다. 이때 시간 부분은 제공된 달력의 표준 시간대에서 Java 기준 시간인 00:00(자정)으로 설정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getDate 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
