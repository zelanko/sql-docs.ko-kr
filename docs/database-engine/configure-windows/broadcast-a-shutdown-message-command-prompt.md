---
title: 종료 메시지 브로드캐스트(명령 프롬프트) | Microsoft Docs
description: Net send 명령을 사용하여 SQL Server에서 메시지를 브로드캐스팅하는 방법을 알아봅니다. 현재 SQL Server에 연결된 사용자를 확인하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, stopping
- named instances [SQL Server], broadcasting shutdown messages
- shutdown message broadcast
- broadcasting shutdown message
- command prompt [SQL Server], broadcasting shutdown messages
- default instances [SQL Server], broadcasting shutdown messages
- stopping SQL Server
ms.assetid: 9f20ccd5-d952-431d-ba12-339911af9430
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 85d2bac016287afd060cdf727eeea47a6b78d725
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759210"
---
# <a name="broadcast-a-shutdown-message-command-prompt"></a>종료 메시지 브로드캐스트(명령 프롬프트)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 **net send** 명령을 사용하여 종료 메시지를 브로드캐스팅하는 방법에 대해 설명합니다. 사용자가 제시간에 태스크를 완료할 수 있도록 메시지에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 중지 시간을 포함시키세요.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-broadcast-a-shutdown-message"></a>종료 메시지를 브로드캐스팅하려면  
  
1.  명령 프롬프트에서 다음을 입력합니다.  
  
     **net send /users "message"**  
  
     **/users** 옵션은 서버에 연결된 모든 사용자에게 메시지를 보내도록 지정합니다.  
  
> [!NOTE]  
>  **net send** 명령을 사용하려면 보내는 컴퓨터와 받는 컴퓨터 모두에서 메신저 서비스가 실행되고 있어야 합니다. 메신저 서비스는 Windows Server 2003에서 기본적으로 해제되어 있습니다. **net send**에 대한 자세한 내용은 Windows 설명서를 참조하세요.  
  
 네트워크에서는 전자 메일이나 전화로 사용자에게 연락하는 것이 더 적절합니다. 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결된 사용자를 확인하려면 작업 모니터를 사용합니다. 작업 모니터에 대한 자세한 내용은 [작업 모니터](../../relational-databases/performance-monitor/activity-monitor.md) 및 [작업 모니터 열기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진, SQL Server 에이전트 또는 SQL Server Browser 서비스 시작, 중지, 일시 중지, 재개 및 다시 시작](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
  
