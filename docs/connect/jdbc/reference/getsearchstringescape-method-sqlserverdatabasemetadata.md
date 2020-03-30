---
title: getSearchStringEscape 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b65281fbe6ba1f758bdd4e12ae834cee3347842
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67980054"
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>getSearchStringEscape 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  와일드카드 문자를 이스케이프하는 데 사용할 수 있는 **문자열**을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Return Value  
 이스케이프 와일드카드 문자열이 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getSearchStringEscape 메서드는 java.sql.DatabaseMetaData 인터페이스의 getSearchStringEscape 메서드에 의해 지정됩니다.  
  
 이 메서드는 메타데이터 패턴 검색에만 사용되며 "\\"를 반환합니다. **문자열** 검색 패턴은 와일드카드("%" 및 "_")를 이스케이프하고 그 앞에 백슬래시를 추가하여 리터럴로 제공할 수 있습니다. 이렇게 하면 "\\%"는 "[%]"로 변환되고, "\\\_"는 "[\_]"로 변환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
