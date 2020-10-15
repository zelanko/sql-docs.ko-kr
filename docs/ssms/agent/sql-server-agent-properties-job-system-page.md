---
description: SQL Server 에이전트 속성(작업 시스템 페이지)
title: SQL Server 에이전트 속성(작업 시스템 페이지)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a617c4b4737ed08ad3ce2227b6d629c235c26018
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038166"
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server 에이전트 속성(작업 시스템 페이지)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스의 작업 관리 방법을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**시스템 종료 제한 시간 간격(초)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 종료 전 작업 완료 대기 시간(초)을 지정합니다. 지정한 간격을 초과하여 작업이 실행되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 강제로 작업을 중지합니다.  
  
**비관리자 프록시 계정 사용**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 대한 비관리자 프록시 계정을 설정합니다. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 이상 버전에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**사용자 이름**  
비관리자 프록시 계정에 대한 사용자의 이름을 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**암호**  
비관리자 프록시 계정에 대한 사용자의 암호를 입력합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**도메인**  
비관리자 프록시 계정에 대한 사용자의 도메인을 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 구현](../../ssms/agent/implement-jobs.md)  
