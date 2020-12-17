---
description: 경고 속성 - 새 경고(옵션 페이지)
title: 경고 속성 - 새 경고(옵션 페이지)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.options.f1
ms.assetid: 6e4f41aa-832d-46ba-b6b5-cf1d3b15d33f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: cebd4c7204c1f416a40e0ac61bd91212b655eb99
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472414"
---
# <a name="alert-properties---new-alert-options-page"></a>경고 속성 - 새 경고(옵션 페이지)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 대한 옵션을 확인하고 수정할 수 있습니다.  

## <a name="options"></a>옵션  
**전자 메일**  
전자 메일 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
**호출기**  
호출기 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
**Net Send**  
Net Send 알림에 이벤트의 오류 텍스트(있는 경우)를 포함합니다.  
  
**추가로 보낼 알림 메시지**  
알림 메시지에 포함할 추가 텍스트를 입력합니다.  
  
**응답 간격**  
이벤트의 반복된 발생에 대한 지연 시간을 지정합니다. 일부 이벤트는 짧은 기간 동안에 자주 발생할 수 있습니다. 이 경우 이벤트가 발생했음을 알고 싶기는 하지만 모든 이벤트에 응답하고 싶지는 않을 수 있습니다. 이 옵션을 사용하여 제한 시간을 지정할 수 있습니다. 지연 시간을 지정하면 경고 이벤트에 응답한 후 이벤트 발생 여부에 관계없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 지정된 지연 시간 동안 대기한 후 다시 응답합니다.  
  
**분**  
지연 시간을 분 단위로 지정합니다. 이벤트가 발생할 때마다 응답하려면 0분 0초를 지정합니다.  
  
**초**  
지연 시간을 초 단위로 지정합니다. 이벤트가 발생할 때마다 응답하려면 0분 0초를 지정합니다.  
  
## <a name="see-also"></a>참고 항목  
[경고](../../ssms/agent/alerts.md)  
