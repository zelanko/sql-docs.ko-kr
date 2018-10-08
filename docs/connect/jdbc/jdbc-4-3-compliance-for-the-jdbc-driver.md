---
title: JDBC 4.3 JDBC 드라이버에 대 한 준수 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f38b700f998babd9af54c3bf8a27409a4d2b6ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623941"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.3 준수

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> SQL Server용 Microsoft JDBC Driver 6.4 이전 버전은 JDBC(Java Database Connectivity) API 4.2 사양만을 준수합니다. 6.4 릴리스 포함 이전 버전에는 이 섹션이 적용되지 않습니다.

버전 6.4, SQL Server 용 Microsoft JDBC Driver는 JAVA 9 호환 않으며 `SQLFeatureNotSupportedException` 메서드를 구현 하는 새로운 JDBC 4.3 Api에 대 한 합니다.

Microsoft JDBC 드라이버 7.0 SQL Server 릴리스를 사용 하 여 드라이버는 이제 JAVA 10 호환 및 지원 아래 설명한 Api. 드라이버 throw `SQLFeatureNotSupportedException` JDBC 4.3 사양에서 구현 되지 않은 다른 방법에 대 한 합니다.

|새 API|설명|중요한 구현|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|이 연결에서 요청을 작업 하는 독립적인 단위를 시작 하는 드라이버에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)을 참조하세요.|공용 API 메서드를 통해 수정할 수 있는 연결 필드의 값을 저장: `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`를 `sendTimeAsDatetime`를 `statementPoolingCacheSize`, `disableStatementPooling`를 `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall `, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert `.|
|void java.sql.connection.endRequest()|작업에서 독립적인 단위는 요청이 완료 되었음을 드라이버에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)을 참조하세요.|작업 단위 중에 생성 되는 문을 닫히고 열려 있는 모든 트랜잭션을 롤백합니다. 메서드는 또한 위에 나열 된 연결 필드에 변경 내용이 되돌립니다.|
