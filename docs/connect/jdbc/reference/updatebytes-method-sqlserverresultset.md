---
title: updateBytes 메서드(SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3050c836-fbb3-4475-99e5-05637a48a932
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f63a21b69bc0650dd6d46f0b0e15708f089af537
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784211"
---
# <a name="updatebytes-method-sqlserverresultset"></a>updateBytes 메서드(SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 열을 **byte** 값의 배열로 업데이트합니다.  
  
## <a name="overload-list"></a>오버로드 목록  
  
|속성|설명|  
|----------|-----------------|  
|[updateBytes(int, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-int-byte.md)|열 인덱스가 지정된 경우 지정된 열을 **byte** 값의 배열로 업데이트합니다.|  
|[updateBytes(java.lang.String, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-java-lang-string-byte.md)|열 이름이 지정된 경우 지정된 열을 **byte** 값의 배열로 업데이트합니다.|  
  
## <a name="remarks"></a>Remarks  
 이전 버전의 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서는 SQLServerResultSet.updateBytes를 사용하여 바이트 배열과 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 **date**, **time**, **datetime2** 또는 **datetimeoffset** 간에 값을 변환할 수 있었습니다. 이제 이 메서드와 이러한 데이터 형식을 함께 사용하면 변환이 지원되지 않음을 나타내는 예외가 발생합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
