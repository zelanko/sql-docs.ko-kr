---
title: 경고 속성 - 새 경고(응답 페이지)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3266ae4e031088a0db6155d5ee20e792b6d9365c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749225"
---
# <a name="alert-properties---new-alert-response-page"></a>경고 속성 - 새 경고(응답 페이지)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고에 대한 응답으로 실행할 작업을 지정하거나 알림을 받을 운영자 목록을 가져올 수 있습니다.  

## <a name="options"></a>옵션  
**작업 실행**  
**작업 목록**, **새 작업** 및 **작업 보기** 옵션을 설정합니다.  
  
**새 작업**  
**새 작업** 대화 상자를 엽니다. **작업 실행** 이 선택되어 있지 않으면 이 단추를 사용할 수 없습니다.  
  
**작업 보기**  
선택한 작업을 확인하거나 수정합니다. **작업 실행** 이 선택되어 있지 않으면 이 옵션을 사용할 수 없습니다.  
  
**운영자에게 알림**  
운영자를 추가, 제거 또는 변경할 수 있는 컨트롤을 설정합니다.  
  
**운영자 목록**  
경고 발생 시 알림을 받을 운영자의 목록입니다. 알림 방법을 지정하려면 운영자 이름 다음에 표시된 **전자 메일**, **호출기**또는 **Net Send** 확인란을 선택합니다. **운영자에게 알림** 이 선택되어 있지 않으면 이 옵션을 사용할 수 없습니다.  
  
**전자 메일**  
전자 메일을 사용하여 운영자에게 알립니다.  
  
**호출기**  
호출기 전자 메일 주소를 사용하여 운영자에게 알립니다.  
  
**Net Send**  
**net send** 를 사용하여 운영자에 게 알립니다.  
  
**새 운영자**  
새 운영자를 만드는 데 사용할 수 있는 **새 운영자** 대화 상자를 표시합니다.  
  
**운영자 보기**  
현재 선택된 운영자에 대한 **속성** 대화 상자를 표시합니다. **운영자 속성** 대화 상자에서 운영자 속성을 확인 및 수정할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[경고](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[경고](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
