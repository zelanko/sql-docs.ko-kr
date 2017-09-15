---
title: "isSparseColumnSet 메서드 (SQLServerResultSetMetaData) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 69506041a0aca549c4f1a36bce26b87ad9426e5c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>isSparseColumnSet 메서드(SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  결과 집합의 열이 스파스 열 집합인지 여부를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *열*  
  
 열의 인덱스(1부터 시작)입니다.  
  
## <a name="return-value"></a>반환 값  
 **true 이면** 결과 집합의 열은 스파스 열 집합, 그렇지 않은 경우 **false**합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 데이터베이스의 정보를 검색하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQLServerResultSetMetaData 메서드](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData 멤버](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData 클래스](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
