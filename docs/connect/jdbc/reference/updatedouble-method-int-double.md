---
title: updateDouble 메서드 (int, double) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDouble (int, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90c47643-e27e-425d-85a0-63866f858367
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 343a39fbe3f7f98717beb7044b6faab802eaac51
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999023"
---
# <a name="updatedouble-method-int-double"></a>updateDouble 메서드(int, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  열 인덱스가 지정된 경우 지정된 열을 **double** 값으로 업데이트합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void updateDouble(int index,  
                         double x)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *index*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
 *x*  
  
 **Double** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 updateDouble 메서드는 java.sql.ResultSet 인터페이스의 updateDouble 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [updateDouble 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
