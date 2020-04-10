---
title: getExtraNameCharacters 메서드(SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExtraNameCharacters
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a22becfe-0f07-4a15-8d11-06d4054b2369
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 346876c1da1322535b7f9802e2e2a9b82064ab5c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924871"
---
# <a name="getextranamecharacters-method-sqlserverdatabasemetadata"></a>getExtraNameCharacters 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  따옴표가 없는 식별자 이름에서 사용할 수 있는 모든 추가 문자(예: a-z, A-Z, 0-9 및 _ 이외의 문자)를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.lang.String getExtraNameCharacters()  
```  
  
## <a name="return-value"></a>Return Value  
 추가 문자가 들어 있는 **문자열**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getExtraNameCharacters 메서드는 java.sql.DatabaseMetaData 인터페이스의 getExtraNameCharacters 메서드에 의해 지정됩니다.  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 데이터베이스와 함께 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 사용할 경우 이 메서드는 $, # 및 \@ 추가 문자를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
