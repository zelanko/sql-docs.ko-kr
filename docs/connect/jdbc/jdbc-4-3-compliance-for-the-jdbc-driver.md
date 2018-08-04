---
title: JDBC 4.3 JDBC 드라이버에 대 한 준수 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f529c88044444f3fb6e428b6c69f5a5cf5917251
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278914"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.3 준수
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  SQL Server용 Microsoft JDBC Driver 6.4 이전 버전은 JDBC(Java Database Connectivity) API 4.2 사양을 준수합니다. 6.4 릴리스 이전 버전에는 이 섹션이 적용되지 않습니다.  
  
 버전 6.4, SQL Server 용 Microsoft JDBC Driver는 JAVA 10과 호환 되지만 JDBC API 4.3 사양을 완벽 하 게 준수 하지 않는. 드라이버는 구현 되지 않은 메서드에 대 한 SQLFeatureNotSupportedException을 throw합니다. 
 
 다음과 같은 JDBC 4.3 API 메서드는 SQL Server 용 Microsoft JDBC Driver 6.4에 구현 됩니다.
 
  **SQLServerConnection 클래스**  
  
|새 메서드|설명|중요한 구현|  
|-----------------|-----------------|-------------------------------|  
|void beginrequest)|이 연결에서 요청을 작업 하는 독립적인 단위를 시작 하는 드라이버에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)을 참조하세요.|공용 API 메서드를 통해 수정할 수 있는 연결 필드의 값을 저장: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`를 `sendTimeAsDatetime`를 `statementPoolingCacheSize`, `disableStatementPooling`를 `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall `, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void endRequest()|작업에서 독립적인 단위는 요청이 완료 되었음을 드라이버에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)을 참조하세요.|작업 단위 중에 생성 되는 문을 닫히고 열려 있는 모든 트랜잭션을 롤백합니다. 메서드는 또한 위에 나열 된 연결 필드에 변경 내용이 되돌립니다.|