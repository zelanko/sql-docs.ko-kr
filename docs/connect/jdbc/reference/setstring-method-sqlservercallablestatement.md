---
title: setString 메서드 (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff224739664e55a1e05d45f684f199969903fc04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972646"
---
# <a name="setstring-method-sqlservercallablestatement"></a>setString 메서드(SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  지정된 매개 변수를 지정된 Java **문자열** 값으로 설정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *sCol*  
  
 매개 변수의 이름을 포함하는 **문자열**입니다.  
  
 *s*  
  
 **문자열** 값입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 setString 메서드는 java.sql.CallableStatement 인터페이스의 setString 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]에서 대상 형식이 이진 파일임을 인식할 수 있는 경우에만 문자열에서 이진 파일로의 변환이 수행됩니다. JDBC 드라이버에서 기본 형식을 인식할 수 없는 경우에 **문자열** 리터럴을 전달하고 서버에서 변환을 수행할 수 없는 경우 서버 오류를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerCallableStatement 멤버](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement 클래스](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
