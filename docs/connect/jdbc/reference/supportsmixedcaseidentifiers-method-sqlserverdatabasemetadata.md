---
title: supportsMixedCaseIdentifiers 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0f68d9f7-0d8d-4d8d-9188-14e253a2576a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62596595a155b900a69595b71c11dc1ca37b185a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815822"
---
# <a name="supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>supportsMixedCaseIdentifiers 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 데이터베이스에서 따옴표로 묶이지 않고 대/소문자가 혼합된 SQL 식별자를 대/소문자가 구분되는 것으로 처리하고 대/소문자가 혼합된 형식으로 저장하는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>반환 값  
 식별자가 대/소문자가 혼합된 형식으로 저장되면 이고, 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 이 supportsMixedCaseIdentifiers 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsMixedCaseIdentifiers 메서드에 의해 지정 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
