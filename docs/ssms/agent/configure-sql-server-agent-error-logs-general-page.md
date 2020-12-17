---
description: SQL Server 에이전트 오류 로그 구성(일반 페이지)
title: 오류 로그 구성(일반 페이지)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 85ae0e4833a1f17f2bd4a795886be8453d61bafd
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482244"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>SQL Server 에이전트 오류 로그 구성(일반 페이지)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 화면을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 오류 로깅의 설정을 확인하고 업데이트할 수 있습니다.  
  
## <a name="options"></a>옵션  
**오류 로그 파일**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 오류 로그를 쓸 파일을 지정합니다.  
  
**...**  
오류 로그 파일을 찾아봅니다.  
  
**OEM 오류 로그 쓰기**  
오류 로그 파일을 비유니코드 파일로 작성합니다. 이렇게 하면 로그 파일에서 사용하는 디스크 공간의 양이 줄어듭니다. 그러나 이 옵션을 설정하면 유니코드 데이터가 포함된 메시지를 읽기가 어려울 수 있습니다.  
  
**Errors**  
로그 파일에 오류 및 정보 메시지만 기록합니다.  
  
**경고**  
로그 파일에 경고 및 정보 메시지만 기록합니다.  
  
**정보**  
로그 파일에 정보 메시지만 기록합니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server 에이전트 오류 로그](../../ssms/agent/sql-server-agent-error-log.md)  
