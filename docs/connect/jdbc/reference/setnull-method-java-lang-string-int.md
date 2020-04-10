---
title: setNull 메서드(java.lang.String, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setNull (java.lang.String, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e1d7e267-d9de-407a-b1a9-abdc2623478d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2601c62446871d8abfb76f52e07b76600cbd054
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920893"
---
# <a name="setnull-method-javalangstring-int"></a>setNull 메서드(java.lang.String, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  설정할 매개 변수 형식이 지정된 경우 지정된 매개 변수를 null 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setNull(java.lang.String sCol,  
                    int nType)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
 *nType*  
  
 java.sql.Types에 의해 정의된 JDBC 형식 코드입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 setNull 메서드는 java.sql.CallableStatement 인터페이스의 setNull 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [setNull 메서드(SQLServerCallableStatement)](../../../connect/jdbc/reference/setnull-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
