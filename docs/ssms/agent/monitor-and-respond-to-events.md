---
title: 이벤트 모니터링 및 응답 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 47f88b65cb7ad746f3e3ab1ab7b0c7ad95de1196
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715067"
---
# <a name="monitor-and-respond-to-events"></a>이벤트 모니터링 및 응답
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 *의 메시지, 특정 성능 조건 및 WMI(Windows Management Instrumentation) 이벤트와 같은*이벤트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 모니터링하고 자동으로 응답할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
[경고](../../ssms/agent/alerts.md)  
경고 명명 방법과 경고가 응답할 이벤트나 성능 조건을 선택하는 방법을 설명합니다.  
  
[사용자 정의 이벤트 만들기](../../ssms/agent/create-a-user-defined-event.md)  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 미리 정의된 이벤트 이외의 이벤트를 만드는 방법을 설명합니다.  
  
[연산자](../../ssms/agent/operators.md)  
작업 실패 또는 작업 성공 시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 알림을 보내기 위해 사용할 수 있는 관리자용 별칭을 만드는 방법을 설명합니다.  
  
## <a name="about-monitoring-and-responding-to-events"></a>이벤트 모니터링 및 응답 정보  
이벤트에 대한 자동화된 응답을 *경고*라고 합니다. 하나 이상의 이벤트에 대한 경고를 정의하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 이벤트 발생에 응답하는 방법을 지정할 수 있습니다. 경고는 관리자에게 알리거나 작업을 실행하거나 또는 두 가지 방법을 모두 사용하여 이벤트에 응답할 수 있습니다. 경고는 다른 컴퓨터의 Microsoft Windows 응용 프로그램 로그에 이벤트를 전달할 수도 있습니다. 예를 들어 심각도가 19인 이벤트가 발생하면 운영자가 즉시 알림을 받을 수 있도록 지정할 수 있습니다. 경고를 정의하면 데이터베이스 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 보다 효과적으로 모니터링하고 관리할 수 있습니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 경고가 정의된 이벤트에만 응답합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 이벤트를 모니터링하기 위해 사용하는 방법은 이벤트 유형에 따라 달라집니다.  
  
성능 카운터에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고가 정의되어 있는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 성능 카운터를 직접 모니터링합니다. WMI 이벤트의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 WMI 이벤트에 대한 이벤트 쿼리를 등록합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 메시지에 응답하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 Windows 응용 프로그램 로그를 모니터링합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트는 이 로그에 나타나는 메시지에만 응답할 수 있습니다. 기본적으로 SQL Server는 다음 메시지를 Windows 응용 프로그램 로그에 기록합니다.  
  
-   심각도가 19 이상인 sysmessages 오류  
  
    심각도가 19 이하인 특정 sysmessages 오류도 기록하려면 sp_altermessage 저장 프로시저를 사용하여 그러한 오류를 "항상 기록"하도록 지정하십시오.  
  
-   WITH LOG 구문을 사용하여 호출된 모든 RAISERROR 문  
  
    RAISERROR WITH LOG 사용은 SQL Server 인스턴스의 메시지를 Windows 응용 프로그램 로그에 쓸 때 권장되는 방법입니다.  
  
-   xp_logevent를 사용하여 기록된 모든 응용 프로그램 이벤트  
  
    > [!NOTE]  
    > 응용 프로그램 이벤트를 기록하면 로그 공간이 사용되므로 Windows 응용 프로그램 로그가 최대 크기를 초과할 수 있습니다. 최대 Windows 응용 프로그램 로그 크기를 충분히 크게 설정하여 SQL Server 이벤트 정보가 손실되지 않도록 하십시오.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 메시지를 기록하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 메시지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관리자가 정의한 경고와 비교합니다.  
  
이벤트 원본에 관계 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스는 이벤트에 대한 경고에 지정된 태스크를 수행하여 이벤트에 응답합니다.  
  
## <a name="see-also"></a>참고 항목  
[sp_altermessage](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
