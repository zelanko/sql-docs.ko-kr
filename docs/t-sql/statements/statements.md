---
title: 문 | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bf492b24e1473ce189f39a84096242773b78cc4a
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "82086819"
---
# <a name="transact-sql-statements"></a>Transact-SQL 문

[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

SQL 문은 작업의 원자성 단위이며 완전히 성공하거나 완전히 실패합니다. SQL 문은 식별자, 매개 변수, 변수, 이름, 데이터 형식 및 성공적으로 컴파일되는 SQL 예약어로 구성된 지침 집합입니다. `BeginTransaction` 명령에 트랜잭션 시작이 지정되지 않을 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서는 SQL 문에 대한 *암시적* 트랜잭션을 만듭니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]는 문이 성공하는 경우 항상 암시적 트랜잭션을 커밋하고 명령이 실패하는 경우 암시적 트랜잭션을 롤백합니다.  

문에는 여러 가지 형식이 있습니다. 아마도 가장 중요한 것은 데이터베이스에서 행을 검색하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 하나 이상의 테이블에서 하나 이상의 행 또는 열을 선택할 수 있도록 하는 [SELECT](../queries/select-transact-sql.md)일 것입니다. 이 문서에는 `SELECT` 문 외에 Transact-SQL(T-SQL)과 함께 사용할 문의 범주가 요약되어 있습니다. 왼쪽 탐색 창에 나열된 모든 문을 찾을 수 있습니다.

## <a name="backup-and-restore"></a>백업 및 복원

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

Service Broker는 메시징 및 큐 애플리케이션에 대한 기본 지원을 제공합니다. 자세한 내용은 [Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)를 참조하세요.

## <a name="session-settings"></a>세션 설정

SET 문은 현재 세션이 시간 설정을 어떻게 취급하는지를 결정합니다. 개요에 대해서는 [SET 문](set-statements-transact-sql.md)을 참조합니다.
