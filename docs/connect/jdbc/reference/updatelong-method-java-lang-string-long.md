---
title: updateLong 메서드(java.lang.String, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateLong (java.lang.String, long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6003706-35de-42b1-8f23-899a388adb5b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0b799ab2a32435ed87135cdb231e0565a44ee26
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80901019"
---
# <a name="updatelong-method-javalangstring-long"></a>updateLong 메서드(java.lang.String, long)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 이름이 지정된 경우 지정된 열을 **long** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateLong(java.lang.String columnName,  
                       long x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnName*  
  
 열 이름이 포함된 **문자열**입니다.  
  
 *x*  
  
 **long** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateLong 메서드는 java.sql.ResultSet 인터페이스의 updateLong 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateLong 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
