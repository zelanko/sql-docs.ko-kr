---
title: "SSIS Scale Out 로깅을 위한 계정 변경 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dcedbe0d2c2ef2c2089af1e2a8b31fbeb75ce2fc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="change-the-account-for-scale-out-logging"></a>Scale Out 로깅을 위한 계정 변경
Scale Out에서 패키지를 실행하면 자동 생성된 사용자 **##MS_SSISLogDBWorkerAgentLogin##**을 사용하여 SSISDB에 이벤트 메시지가 기록됩니다. 이 사용자 로그인은 SQL Server 인증을 사용합니다. 계정을 변경하려면 아래 단계를 따릅니다.

## <a name="1-create-a-user-of-ssisdb"></a>1. SSISDB 사용자 만들기
데이터베이스 사용자를 만드는 지침은 [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)를 참조하세요.

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. 데이터베이스 역할 ssis_cluster_worker에 사용자 추가

데이터베이스 역할을 조인하는 지침은 [역할 조인](../../relational-databases/security/authentication-access/join-a-role.md)을 참조하세요.

## <a name="3-update-logging-information-in-ssisdb"></a>3. SSISDB에서 로깅 정보 업데이트
Sql Server 이름 및 연결 문자열을 매개 변수로 사용하여 저장 프로시저 [catalog].[update_logdb_info]를 호출합니다.

#### <a name="example"></a>예제
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. Scale Out Worker 서비스 다시 시작

> [!NOTE]
> 로깅에 Windows 사용자 계정을 사용하는 경우 해당 계정은 Scale Out Worker 서비스를 실행하는 계정과 같은 계정이어야 합니다. 그렇지 않으면 SQL Server 로그인이 실패합니다.
