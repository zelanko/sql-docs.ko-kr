---
title: 작업 속성 - 새 작업(일반 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.general.f1
ms.assetid: b6832840-1c18-4db8-94fc-080db880ae9f
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bb07909f1776684039f0cec6aaa22a1e9ef0cb66
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686907"
---
# <a name="job-properties---new-job-general-page"></a>작업 속성 - 새 작업(일반 페이지)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 일반 속성을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**이름**  
작업 이름을 변경합니다.  
  
**소유자**  
작업의 소유자를 선택합니다.  
  
**범주**  
작업의 범주를 선택합니다.  
  
**...**  
선택한 범주의 작업을 표시합니다.  
  
**설명**  
작업 설명을 변경합니다.  
  
**Enabled**  
작업을 설정합니다. 작업을 설정하지 않은 경우 일정 또는 경고에 따라 작업이 실행되지는 않지만 **sp_start_job** 저장 프로시저를 사용하여 작업을 시작할 수 있습니다.  
  
**원본**  
작업에 사용되는 마스터 서버를 표시합니다. **작업 속성 일반** 페이지에서만 사용할 수 있습니다.  
  
**만든 날짜**  
작업을 만든 날짜와 시간을 표시합니다. **작업 속성 일반** 페이지에서만 사용할 수 있습니다.  
  
**마지막으로 수정한 날짜**  
작업을 마지막으로 수정한 날짜와 시간을 표시합니다. **작업 속성 일반** 페이지에서만 사용할 수 있습니다.  
  
**마지막으로 실행한 날짜**  
마지막으로 작업 실행을 시작한 날짜 및 시간을 표시합니다. **작업 속성 일반** 페이지에서만 사용할 수 있습니다.  
  
**작업 기록 보기**  
작업의 기록을 확인합니다. **작업 속성 일반** 페이지에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 구현](../../ssms/agent/implement-jobs.md)  
[작업 범주 - 작업 범주 관리](../../ssms/agent/job-categories-manage-job-categories.md)  
  
