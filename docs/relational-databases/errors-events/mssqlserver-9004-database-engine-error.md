---
description: MSSQLSERVER_9004
title: MSSQLSERVER_9004 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f9b9a18806a4a91b58d0b30e83e560e8f73f6be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460908"
---
# <a name="mssqlserver_9004"></a>MSSQLSERVER_9004
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|9004|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|LOG_CORRUPT|  
|메시지 텍스트|데이터베이스 '%.*ls'의 로그를 처리하는 동안 오류가 발생했습니다.  가능하면 백업을 사용하여 복원하십시오. 백업이 없을 경우 로그를 다시 만들어야 합니다.|  
  
## <a name="explanation"></a>설명  
롤백, 복구 또는 복제 중 로그를 처리하는 동안 오류가 발생했습니다. 운영 체제에서 발견한 오류이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 발견한 내부 일관성 오류일 수 있습니다.  
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]은 트랜잭션 로그를 읽고 처리할 때 내용 일관성에 대한 논리적 검사를 수행합니다. 로그 헤더, 로그 블록 및 로그 레코드의 모든 측면이 검사되는 것은 아닙니다. 상태 번호는 오류 유형에 대한 자세한 정보를 제공합니다.

 - **상태 1** VLF(가상 로그 파일)의 로그 파일 헤더가 손상되었습니다.  서비스 시작 시 데이터베이스를 시작하는 과정에서 손상된 로그 파일 헤더가 발견되는 경우 오류 로그에 오류 9004만 표시될 수 있습니다. 로그 파일 헤더는 트랜잭션 로그에서 각 VLF의 첫 번째 부분입니다. 로그 파일 헤더는 단일 파일 헤더, 즉 로그 파일의 첫 8KB와 동일하지 않습니다. 로그 파일의 파일 헤더가 손상된 경우 데이터베이스 파일 헤더 페이지 손상과 비슷한 메시지 5172가 반환될 수 있습니다.
 - **상태 2 및 3** RESTORE 작업 중 복구를 수행할 때 로그 블록이 잘못되었습니다.
 - **상태 4~12** 로그 레코드를 처리할 때 로그 블록에 대한 다양한 검사입니다. 여기에는 트랜잭션 로그의 패리티, 섹터 및 기타 일관성에 대한 논리적 검사가 포함됩니다.

대부분의 경우 이 오류는 EventID = 9004인 오류 로그 또는 Windows 애플리케이션 이벤트 로그에만 표시됩니다. 로그를 처리하는 작업이 직접 사용자 명령(예: SQL Server 엔진이 시작될 때 실행되는 복구)을 기반으로 하지 않기 때문입니다. 이러한 상황에서 오류 9004는 종종 오류 3414와 함께 표시됩니다. 그러나 ALTER DATABASE와 같은 일부 쿼리에는 로그 처리가 필요할 수 있으므로 이러한 오류가 표시됩니다. 이 오류는 심각도=21이므로 사용자 세션의 연결이 끊어집니다.

## <a name="cause"></a>원인
오류 9004는 트랜잭션 로그의 내용이 손상되었음을 나타내는 일반 오류입니다. 로그가 일치하지 않게 되는 이유는 SQL Server 엔진이 감지한 데이터베이스 손상 문제와 비슷합니다. 로그 손상의 원인을 찾으려면 가능한 하드웨어, 파일 시스템 및 I/O 문제에 대한 분석을 포함하여 데이터베이스 손상에 사용되는 유사한 기법을 따라야 합니다. DBCC CHECKDB는 해당 작업의 일부로 트랜잭션 로그를 검사하지 않으며 로그 손상 오류를 검색할 수 없습니다. 오류 9004는 SQL Server 엔진 자체에서 발생시킵니다.

## <a name="user-action"></a>사용자 동작  
이 오류를 수정하려면 다음 중 하나를 수행하십시오.  
  
-   **백업에서 복구**:  이 문제에서 복구하려면 알려진 양호한 백업에서 복원하세요. 데이터베이스 또는 로그 백업의 로그 부분에 손상된 내용이 포함되어 있으면 RESTORE 시 9004 오류가 발생할 수 있습니다. 이 경우 백업의 트랜잭션 로그가 손상된 것입니다.
  
-   **로그를 다시 작성**:  백업에서 복원할 수 없는 경우 트랜잭션 로그를 다시 작성하여 데이터베이스를 온라인 상태로 만들 수 있습니다. 트랜잭션 로그를 다시 작성할 경우 발생하는 결과를 정확하게 이해해야 합니다. 여기에는 데이터베이스에서 트랜잭션 일관성 손실이 포함됩니다. 트랜잭션 로그를 다시 작성하는 방법에 대한 자세한 내용은 [데이터베이스 응급 모드에서 오류 해결](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md#resolving-errors-in-database-emergency-mode)을 참조하세요.
  
-   **시스템 문제에 대한 로그를 확인**: 또한 시스템 이벤트 및 오류 로그에서 문제를 일으킬 수 있는 시스템 내부 문제를 확인합니다.  
  
