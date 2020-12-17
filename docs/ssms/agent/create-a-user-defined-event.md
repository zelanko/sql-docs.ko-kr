---
description: 사용자 정의 이벤트 만들기
title: 사용자 정의 이벤트 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: de6830e6256a0cff840d34e179b198803f03016d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464424"
---
# <a name="create-a-user-defined-event"></a>사용자 정의 이벤트 만들기
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 미리 정의된 이벤트 이외의 이벤트를 모니터링하려는 경우 사용자 정의 이벤트를 만들 수 있습니다. 각 사용자 정의 이벤트에 심각도 수준을 할당할 수도 있습니다.  
  
> [!NOTE]  
> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용할 때 각 사용자 정의 이벤트 메시지에 대해 **Windows 애플리케이션 이벤트 로그에 쓰기** 옵션을 선택하여 메시지를 로그에 기록합니다. 기본적으로 심각도가 19보다 낮은 사용자 정의 메시지가 발생하면 이 메시지는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 애플리케이션 로그로 전송되지 않습니다. 심각도 수준이 19보다 낮은 사용자 정의 메시지는 SQL Server 에이전트 경고를 트리거하지 않습니다.  
  
사용자 정의 이벤트에는 고유한 메시지 번호가 필요합니다. 사용자 정의 이벤트의 메시지 번호는 50,000보다 커야 합니다. 이벤트에 대한 메시지는 여러 언어로 정의할 수 있습니다. 그러나 다른 언어로 된 메시지를 추가하려면 먼저 **En-US** 오류 메시지가 있어야 합니다.  
  
여러 언어로 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 환경을 관리하는 경우 지원되는 각 언어로 사용자 정의 메시지를 만드십시오. 예를 들어 영어 서버와 독일어 서버에서 사용할 이벤트 메시지를 새로 만들 경우에 두 서버에 같은 메시지 번호와 심각도를 사용하지만 각각 다른 언어를 할당하십시오.  
  
다음 태스크는 작업에 응답하는 사용자 정의 이벤트와 경고를 만드는 방법을 제공합니다.  
  
**메시지 번호를 기반으로 경고를 만들려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**심각도 수준을 기반으로 경고를 만들려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**경고에 대한 응답을 정의하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)  
  
**사용자 정의 이벤트 오류 메시지를 만들려면**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)  
  
**사용자 정의 이벤트 오류 메시지를 수정하려면**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
**사용자 정의 이벤트 오류 메시지를 삭제하려면**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)  
  
**경고를 비활성화하거나 다시 활성화하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
[sp_update_alert(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
