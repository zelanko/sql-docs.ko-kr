---
description: MSSQLSERVER_3023
title: MSSQLSERVER_3023
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3023 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0197c7e5b75164615572e4041a5b348a4d5abcc4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418796"
---
# <a name="mssqlserver_3023"></a>MSSQLSERVER_3023
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|3023|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|DB_IN_USE_DUMP|
|메시지 텍스트|데이터베이스에 대한 백업 및 파일 조작 작업(예: ALTER DATABASE ADD FILE)은 직렬화되어야 합니다. 현재 백업 또는 파일 조작 작업이 완료되면 문을 다시 실행하세요.|
||

## <a name="explanation"></a>설명

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 Backup, shrink 또는 alter database 명령을 실행하려고 하면 다음과 같은 메시지가 나타납니다.

> 메시지 3023, 수준 16, 상태 2, 줄 1  
데이터베이스에 대한 백업 및 파일 조작 작업(예: ALTER DATABASE ADD FILE)은 직렬화되어야 합니다. 현재 백업 또는 파일 조작 작업이 완료되면 문을 다시 실행하십시오.

> 메시지 3013, 수준 16, 상태 1, 줄 1  
백업 데이터베이스가 비정상적으로 종료됩니다.

또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 다음과 같은 메시지가 포함됩니다.

> \<Datetime> 백업 오류: 3041, 심각도: 16, 상태: 1.  
\<Datetime> 백업. BACKUP에서 BACKUP DATABASE MyDatabase WITH DIFFERENTIAL 명령을 완료하지 못했습니다. 자세한 내용은 백업 애플리케이션 로그를 확인하십시오.

또한 `sys.dm_exec_requests` 또는 `sys.dm_os_waiting_tasks`와 같은 다양한 DMV(동적 관리 뷰)에서 명령의 상태를 살펴보면 관련 명령에서 `wait_type = LCK_M_U` 및 `wait_resource = DATABASE: <id> [BULKOP_BACKUP_DB]`가 발생하는 것을 확인할 수 있습니다.

## <a name="possible-causes"></a>가능한 원인

데이터베이스에 대해 전체 데이터베이스 백업이 현재 진행 중인 경우 허용되거나 허용되지 않는 작업과 관련된 몇 가지 규칙이 있습니다. 몇 가지 예는 다음과 같습니다.

- 한 번에 하나의 데이터 백업만 수행할 수 있습니다(전체 데이터베이스 백업을 수행하는 경우 차등 또는 증분 백업을 동시에 수행할 수 없음).
- 한 번에 하나의 로그 백업만 수행할 수 있습니다(전체 데이터베이스 백업을 수행하는 경우 로그 백업을 수행할 수 있음).
- 백업을 수행하는 동안에는 데이터베이스에 파일을 추가하거나 삭제할 수 없습니다.
- 데이터베이스 백업을 수행하는 동안에는 파일을 축소할 수 없습니다.
- 백업을 수행하는 동안에는 제한된 복구 모델 변경만 허용됩니다.

충돌하는 작업을 수행하는 명령을 실행할 경우 “설명” 섹션에 언급된 잠금 대기가 발생하고 3023 및 3041 메시지가 표시됩니다.

## <a name="user-action"></a>사용자 조치

다양한 데이터베이스 유지 관리 작업 일정을 확인하고 작업 또는 명령이 서로 충돌하지 않도록 일정을 조정합니다.

## <a name="more-information"></a>자세한 정보

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 백업 시작 시간 및 종료 시간을 `msdb` 데이터베이스에 기록합니다. 백업 기록을 검사하여 전체 데이터베이스 백업이 수행되는 동안 증분 백업을 시도하여 오류가 발생했는지 여부를 확인할 수 있습니다. 다음 쿼리를 사용하면 이 프로세스에 도움이 됩니다.

```sql
select database_name, type, backup_start_date, backup_finish_date
from msdb.dbo.backupset
order by database_name, type, backup_start_date, backup_finish_date
go
```

SQL Profiler 추적의 **사용자 오류 메시지** 이벤트 또는 확장 이벤트의 **error_reported** 이벤트를 사용하여 백업 또는 기타 유지 관리 명령을 시작한 애플리케이션에 보고되는 3023 메시지를 추적할 수도 있습니다.
