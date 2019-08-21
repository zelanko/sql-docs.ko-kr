---
title: Jdbc 드라이버에 대 한 JDBC 4.3 준수 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed9b10ad9e9a927789505c7d7327c6cf4d1ff3c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027940"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.3 준수

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> SQL Server용 Microsoft JDBC Driver 6.4 이전 버전은 JDBC(Java Database Connectivity) API 4.2 사양만을 준수합니다. 6\.4 릴리스 포함 이전 버전에는 이 섹션이 적용되지 않습니다.

버전 6.4부터 SQL Server 용 Microsoft JDBC Driver는 JAVA 9와 호환 되며 구현 되지 `SQLFeatureNotSupportedException` 않은 메서드를 포함 하는 새 JDBC 4.3 api에 대해 throw 됩니다.

SQL Server 릴리스에 대 한 Microsoft JDBC Driver 7.0를 사용 하 여 드라이버는 이제 JAVA 10과 호환 되며 아래에서 언급 한 Api를 지원 합니다. 드라이버는 JDBC `SQLFeatureNotSupportedException` 4.3 사양에서 구현 되지 않은 다른 메서드를 throw 합니다.

|새 API|설명|중요한 구현|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|이 연결에서 시작 하는 요청 (독립적인 작업 단위)에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)을 참조하세요.|공용 API 메서드 ( `databaseAutoCommitMode` ,`statementPoolingCacheSize`,, `holdability`,, ,,,,)를통해수정할수있는연결필드의값을저장합니다.`sendTimeAsDatetime` `disableStatementPooling` `networkTimeout` `transactionIsolationLevel` `serverPreparedStatementDiscardThreshold` `enablePrepareOnFirstPreparedStatementCall` `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|독립적인 작업 단위 요청이 완료 된 드라이버에 대 한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)을 참조하세요.|작업 단위 중에 만들어진 문을 닫고 열려 있는 모든 트랜잭션을 롤백합니다. 또한이 메서드는 위에 나열 된 연결 필드의 변경 내용을 되돌립니다.|
