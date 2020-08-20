---
description: MSSQL_ENG024070
title: MSSQL_ENG024070 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 77cd48a142248d7c969c2658cbbbf4ac20536ed2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493956"
---
# <a name="mssql_eng024070"></a>MSSQL_ENG024070
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|24070|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|클라이언트에 필수 권한이 없습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 복제가 사용 중인지 여부에 관계없이 발생할 수 있는 일반 오류입니다. 복제 토폴로지의 서버에서 이 오류는 일반적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 대신 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 서비스 제어 관리자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 계정을 변경한 경우에 발생합니다. 해당 서비스 계정을 변경한 후 에이전트 작업을 실행하려고 하면 작업이 실패하고 다음과 유사한 오류 메시지가 나타날 수 있습니다.  
  
 `Executed as user: \<UserAccount>. Replication-Replication Snapshot Subsystem: agent \<AgentName> failed. Executed as user: \<UserAccount>. A required privilege is not held by the client. The step failed. [SQLSTATE 42000] (Error 14151). The step failed.`  
  
 이 문제는 Windows 서비스 제어 관리자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 새 서비스 계정에 필요한 권한을 부여할 수 없기 때문에 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
 앞으로 이 문제가 발생하지 않도록 하려면 항상 Windows 서비스 제어 관리자 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스 계정과 암호를 변경해야 합니다.  
  
 이 문제를 해결하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 서비스 계정을 다시 원래 계정으로 변경합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 새 계정으로 변경합니다. 이렇게 하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 다음 보안 그룹에 새 계정을 추가합니다.  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 이 보안 그룹의 멤버가 되는 새 사용자 계정에는 복제 에이전트 작업을 실행하는 데 필요한 권한이 부여됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [복제의 로그인 및 암호 관리](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)  
  
  
