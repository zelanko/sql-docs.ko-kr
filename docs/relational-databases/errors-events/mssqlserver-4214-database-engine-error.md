---
description: MSSQLSERVER_
title: MSSQLSERVER_4214
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4214 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0a04ec00e94dca9a4d940a3b0182123f0716d472
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418843"
---
# <a name="mssqlserver_4214"></a>MSSQLSERVER_4214
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|4214|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|DMPX_NODBBACKUP|
|메시지 텍스트|현재 데이터베이스 백업이 없으므로 BACKUP LOG를 수행할 수 없습니다.|
||

## <a name="explanation"></a>설명

전체 데이터베이스 백업을 수행하기 전에 트랜잭션 로그 백업을 시도하면 오류가 발생합니다. 데이터베이스의 트랜잭션 로그를 백업하기 전에 전체 데이터베이스 백업을 수행해야 합니다. 또한 오류 로그에 다음 메시지가 표시됩니다.

> \<Datetime> 백업 오류: 3041, 심각도: 16, 상태: 1.  
\<Datetime> 백업. BACKUP에서 BACKUP LOG \<db_name> 명령을 완료하지 못했습니다. 자세한 내용은 백업 애플리케이션 로그를 확인하십시오.

## <a name="user-action"></a>사용자 조치

데이터베이스의 트랜잭션 로그를 백업하기 전에 전체 데이터베이스 백업을 수행합니다.

## <a name="more-information"></a>자세한 정보

자세한 내용은 다음을 참조하세요. [SQL Server 데이터베이스 백업 및 복원](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases)