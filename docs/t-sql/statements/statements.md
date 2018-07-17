---
title: 문 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: 7
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 07828132cb2413617b6b0d1141ae9a440e612559
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37790394"
---
# <a name="transact-sql-statements"></a>Transact-SQL 문
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

이 참조 항목에는 TRANSACT-SQL(T-SQL)와 함께 사용할 문의 범주가 요약되어 있습니다. 왼쪽 탐색 창에 나열된 모든 문을 찾을 수 있습니다.

## <a name="backup-and-restore"></a>Backup 및 Restore 메서드
Backup 및 Restore 문은 백업을 만들고 백업에서 복원하는 방법을 제공합니다.  자세한 내용은 [백업 및 복원 개요](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)를 참조하세요.

## <a name="data-definition-language"></a>DDL(데이터 정의 언어)
DDL(데이터 정의 언어) 문은 데이터 구조를 정의합니다. 이 문을 사용하여 데이터베이스에서 데이터 구조를 생성, 변경 또는 삭제합니다.
- ALTER
- 데이터 정렬
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>DML(데이터 조작 언어)
DML(데이터 조작 언어)는 데이터베이스에 저장된 정보에 영향을 줍니다. 이러한 문을 사용하여 데이터베이스에서 행을 삽입, 업데이트 및 변경합니다.

- BULK INSERT
- Delete
- INSERT
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>사용 권한 문
사용 권한 문은 사용자와 로그인이 데이터에 액세스하고 작업을 수행할 수 있는지를 결정합니다. 인증 및 액세스에 대한 자세한 내용은 [보안 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)를 참조합니다.

## <a name="service-broker-statements"></a>Service Broker 문
Service Broker는 메시징 및 큐 응용 프로그램에 대한 기본 지원을 제공합니다. 자세한 내용은 [Service Broker](../../relational-databases/service-broker/event-notifications.md)를 참조하세요.

## <a name="session-settings"></a>세션 설정
SET 문은 현재 세션이 시간 설정을 어떻게 취급하는지를 결정합니다. 개요에 대해서는 [SET 문](set-statements-transact-sql.md)을 참조합니다.
