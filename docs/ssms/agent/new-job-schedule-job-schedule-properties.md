---
description: 새 작업 일정 - 작업 일정 속성
title: 새 작업 일정 - 작업 일정 속성
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.scheduleproperties.f1
- sql13.swb.maint.editrecurringjobsched.f1
ms.assetid: 5c0b1bc9-dd87-49cc-b0dd-75d0d922b177
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 68fde830b44cfb922c9908a75c62c4fbb86d3001
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402572"
---
# <a name="new-job-schedule---job-schedule-properties"></a>새 작업 일정 - 작업 일정 속성
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 일정 속성을 확인하고 변경할 수 있습니다.  
  
## <a name="options"></a>옵션  
**이름**  
새 일정 이름을 입력합니다.  
  
**이 일정 내의 작업**  
일정을 사용하는 작업을 표시합니다.  
  
**일정 유형**  
일정 유형을 선택합니다.  
  
**Enabled**  
일정을 사용하거나 사용하지 않으려면 선택합니다.  
  
## <a name="recurring-schedule-types-options"></a>되풀이 일정 유형 옵션  
**되풀이**  
일정 되풀이 간격을 선택합니다.  
  
**매**  
일정 되풀이 간격을 일 또는 주 단위(수)로 선택합니다. 월별 되풀이 일정에는 이 옵션을 사용할 수 없습니다.  
  
**월요일**  
월요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**화요일**  
화요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**수요일**  
수요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**목요일**  
목요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**금요일**  
금요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**토요일**  
토요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**일요일**  
일요일에 작업이 수행되도록 설정합니다. 주별 되풀이 일정에만 사용할 수 있습니다.  
  
**Day**  
일정이 시작되는 날짜를 선택합니다. 월별 되풀이 일정에만 사용할 수 있습니다.  
  
**일 /**  
일정 되풀이 간격을 월 단위(수)로 선택합니다. 월별 되풀이 일정에만 사용할 수 있습니다.  
  
**이**  
해당 월의 특정 주에 있는 특정 요일에 대한 일정을 지정합니다. 월별 되풀이 일정에만 사용할 수 있습니다.  
  
**한 번 수행**  
매일 작업이 수행되도록 시간을 설정합니다.  
  
**되풀이 수행**  
작업 발생 간격을 시, 분 또는 초 단위(수)로 설정합니다.  
  
**시작 날짜**  
이 일정을 개시할 날짜를 설정합니다.  
  
**종료 날짜**  
일정을 종료할 날짜를 설정합니다.  
  
**종료 날짜 없음**  
일정을 무기한 유지하도록 지정합니다.  
  
## <a name="one-time-schedule-types-options"></a>일회 일정 유형 옵션  
**Date**  
작업을 실행할 날짜를 선택합니다.  
  
**Time**  
작업을 실행할 시간을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[일정을 만들고 작업에 연결](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[작업 예약](../../ssms/agent/schedule-a-job.md)  
