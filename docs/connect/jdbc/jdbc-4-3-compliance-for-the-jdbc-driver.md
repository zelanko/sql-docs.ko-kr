---
title: JDBC 드라이버의 JDBC 4.3 준수 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 099664892564a6b38e270f934cb3208029fdd05f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928355"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 드라이버의 JDBC 4.3 준수

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> SQL Server용 Microsoft JDBC Driver 6.4 이전 버전은 JDBC(Java Database Connectivity) API 4.2 사양만을 준수합니다. 6\.4 릴리스 포함 이전 버전에는 이 섹션이 적용되지 않습니다.

버전 6.4부터 Microsoft JDBC Driver for SQL Server는 JAVA 9와 호환되며 구현되지 않은 메서드가 있는 새로운 JDBC 4.3 API에 대해 `SQLFeatureNotSupportedException`을 throw합니다.

Microsoft JDBC Driver 7.0 for SQL Server 릴리스에서는 이제 드라이버가 JAVA 10과 호환되며 아래 언급된 API를 지원합니다. 드라이버는 JDBC 4.3 사양의 다른 구현되지 않은 메서드에 대해 `SQLFeatureNotSupportedException`를 throw합니다.

|새 API|Description|중요한 구현|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|이 연결에서 시작하는 요청(독립적인 작업 단위)에 대한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)을 참조하세요.|다음 공용 API 메서드를 통해 수정할 수 있는 연결 필드의 값을 저장합니다. `databaseAutoCommitMode`, `transactionIsolationLevel`, `networkTimeout`, `holdability`, `sendTimeAsDatetime`, `statementPoolingCacheSize`, `disableStatementPooling`, `serverPreparedStatementDiscardThreshold`, `enablePrepareOnFirstPreparedStatementCall`, `catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|요청(독립적인 작업 단위)이 완료된 드라이버에 대한 힌트입니다. 자세한 내용은 [java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)을 참조하세요.|작업 단위 중에 만들어진 문을 닫고 열려 있는 모든 트랜잭션을 롤백합니다. 또한 이 메서드는 위에 나열된 연결 필드의 변경 내용을 되돌립니다.|
