---
title: updateString 메서드(int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateString (int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f8d2f620-0cdf-4a3b-8af4-5e8c4462a42d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 12431fe119839337d934b93f76ce64133137b8e2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80919603"
---
# <a name="updatestring-method-int-javalangstring"></a>updateString 메서드(int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정된 경우 지정된 열을 **문자열** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateString(int index,  
                         java.lang.String x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 **String** 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 updateString 메서드는 java.sql.ResultSet 인터페이스의 updateString 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateString 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
