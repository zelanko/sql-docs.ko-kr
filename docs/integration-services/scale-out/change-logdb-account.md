---
title: "SSIS 스케일 아웃 로깅에 대 한 계정을 변경 | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ec785459e5f9585776d83cde3f460c1e79367e46
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="change-the-account-for-scale-out-logging"></a>스케일 아웃 로깅 위한 계정 변경
자동 생성 된 사용자와 SSISDB에 이벤트 메시지가 기록 된다 스케일 아웃에 패키지를 실행할 때 **# # MS_SSISLogDBWorkerAgentLogin # #**합니다. 이 사용자의 로그인 SQL Server 인증을 사용 합니다. 변경 하려면 다음 단계를 다음과 같이 계정:

## <a name="1-create-a-user-of-ssisdb"></a>1. SSISDB 사용자 만들기
데이터베이스 사용자를 만드는 지침은 [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)합니다.

## <a name="2-add-the-user-to-database-role-ssisclusterworker"></a>2. 데이터베이스 역할 ssis_cluster_worker에 사용자 추가

데이터베이스 역할을 조인 지침은 [역할 조인](../../relational-databases/security/authentication-access/join-a-role.md)합니다.

## <a name="3-update-logging-information-in-ssisdb"></a>3. SSISDB에 로깅 정보를 업데이트 합니다.
[Catalog] 저장된 프로시저를 호출 합니다. [update_logdb_info] Sql Server 이름 및 연결 문자열 매개 변수로 사용 합니다.

#### <a name="example"></a>예제
```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-scale-out-worker-service"></a>4. 스케일 아웃 작업자 서비스를 다시 시작

> [!NOTE]
> 로깅에 대 한 Windows 사용자 계정을 사용 하는 경우 스케일 아웃 Worker 서비스를 실행 하는 동일한 계정 이어야 합니다. 그렇지 않으면 SQL Server에 로그인이 실패 합니다.

