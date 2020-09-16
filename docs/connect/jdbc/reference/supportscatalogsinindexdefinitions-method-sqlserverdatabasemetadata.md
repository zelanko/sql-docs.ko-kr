---
description: supportsCatalogsInIndexDefinitions 메서드(SQLServerDatabaseMetaData)
title: supportsCatalogsInIndexDefinitions 메서드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInIndexDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a19423a0-e7b6-4f5c-94be-80ddf3fa4717
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e385c2782ed45ecb2353b01f583e9b3aedc55b7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462493"
---
# <a name="supportscatalogsinindexdefinitions-method-sqlserverdatabasemetadata"></a>supportsCatalogsInIndexDefinitions 메서드(SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  인덱스 정의 문에 카탈로그 이름을 사용할 수 있는지 여부를 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public boolean supportsCatalogsInIndexDefinitions()  
```  
  
## <a name="return-value"></a>Return Value  
 지원되는 경우 **true**입니다. 그렇지 않으면 **false**입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 supportsCatalogsInIndexDefinitions 메서드는 java.sql.DatabaseMetaData 인터페이스의 supportsCatalogsInIndexDefinitions 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQLServerDatabaseMetaData 메서드](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData 멤버](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData 클래스](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
