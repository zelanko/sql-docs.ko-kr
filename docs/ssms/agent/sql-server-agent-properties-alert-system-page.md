---
title: SQL Server 에이전트 속성(경고 시스템 페이지) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cca0a8eb824423c1194e474a4745dda037b13069
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47790262"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>SQL Server 에이전트 속성(경고 시스템 페이지)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고가 보낸 메시지의 설정을 확인하거나 수정할 수 있습니다.  
  
## <a name="options"></a>Options  
**메일 세션**  
이 섹션의 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 메일을 구성합니다.  
  
**메일 프로필 설정**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 메일을 설정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 메일은 설정되지 않습니다.  
  
**메일 시스템**  
사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 메일 시스템을 설정합니다. 데이터베이스 메일  
  
> [!NOTE]  
> 전자 메일 시스템을 변경한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스를 다시 시작해야만 변경 내용이 적용됩니다.  
  
**메일 프로필**  
사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프로필을 설정합니다. **\<새 데이터베이스 메일 프로필...>** 을 선택하여 새 프로필을 만들 수도 있습니다.  
  
**호출기 전자 메일**  
이 섹션의 옵션을 사용하여 호출 시스템에서 사용하는 호출기 주소로 보낼 전자 메일 메시지를 구성할 수 있습니다.  
  
**호출기 전자 메일 주소 형식**  
이 섹션에서는 호출기 전자 메일의 주소 형식과 전자 메일에 포함되는 제목 줄을 지정할 수 있습니다.  
  
**받는 사람 줄**  
메시지의 **받는 사람** 줄에 대한 옵션을 지정합니다.  
  
**Prefix**  
호출기로 전송되는 메시지의 **받는 사람** 줄 시작 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**호출기**  
접두사와 접미사 사이에 메시지의 전자 메일 주소를 포함합니다.  
  
**접미사**  
호출기로 전송되는 메시지의 **받는 사람** 줄 끝 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**참조 줄**  
메시지의 **참조** 줄에 대한 옵션을 지정합니다.  
  
**Prefix**  
호출기로 전송되는 메시지의 **참조** 줄 시작 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**호출기**  
접두사와 접미사 사이에 메시지의 전자 메일 주소를 포함합니다.  
  
**접미사**  
호출기로 전송되는 메시지의 **참조** 줄 끝 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**Subject**  
메시지의 제목에 대한 옵션을 지정합니다.  
  
**Prefix**  
호출기로 전송되는 메시지의 **제목** 줄 시작 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**접미사**  
호출기로 전송되는 메시지의 **제목** 줄 끝 부분에 표시되어야 할 고정 텍스트를 입력합니다.  
  
**알림 메시지에 전자 메일 본문 포함**  
호출기로 전송되는 메시지에 전자 메일 메시지 본문을 포함합니다.  
  
**유사 시 대기 운영자**  
이 섹션에서는 유사 시 대기 운영자에 대한 옵션을 지정할 수 있습니다.  
  
**유사 시 대기 운영자 설정**  
유사 시 대기 운영자를 지정합니다.  
  
**같음**  
유사 시 대기 알림을 받을 운영자의 이름을 설정합니다.  
  
**알림 방법**  
유사 시 대기 운영자에게 알릴 때 사용할 방법을 설정합니다.  
  
**토큰 바꾸기**  
이 섹션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고로 실행되는 작업에 사용할 수 있는 작업 단계 토큰을 설정할 수 있습니다. 작업 단계 토큰에 대한 자세한 내용은 [작업 단계에서 토큰 사용](../../ssms/agent/use-tokens-in-job-steps.md)을 참조하세요.  
  
> [!IMPORTANT]  
> Windows 이벤트 로그에 대한 쓰기 권한이 있는 모든 Windows 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고로 활성화되는 작업 단계에 액세스할 수 있습니다. 이러한 보안상 위험을 방지하기 위해 경고로 활성화되는 작업에 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 토큰은 기본적으로 해제됩니다. 이러한 토큰은 **$(A-DBN)**, **$(A-SVR)**, **$(A-ERR)**, **$(A-SEV)** 및 **$(A-MSG)** 입니다.  
>   
> 이러한 토큰을 사용해야 하는 경우 토큰을 설정하기 전에 Administrators 그룹과 같은 트러스트된 Windows 보안 그룹의 멤버만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 컴퓨터의 이벤트 로그에 대한 쓰기 권한을 가지도록 합니다.  
  
**경고에 대한 모든 응답 작업에 대해 토큰 바꾸기**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 경고로 활성화되는 작업에 대해 토큰 바꾸기를 설정하려면 이 확인란을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
[연산자](../../ssms/agent/operators.md)  
[데이터베이스 메일을 사용하도록 SQL Server 에이전트 메일 구성](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
[데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)  
  
