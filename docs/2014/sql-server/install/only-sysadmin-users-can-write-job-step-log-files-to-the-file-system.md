---
title: Sysadmin 사용자 파일 시스템에 작업 단계 로그 파일에 기록할 수만 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e0b7638bbbf33cdd820467cd21edc40a6f5c42ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093438"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>sysadmin 사용자만 작업 단계 로그 파일을 파일 시스템에 기록할 수 있습니다.
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 선택적으로 각 작업 단계에 대한 로그를 기록합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트의 멤버에 의해 소유 하는 작업에 대 한 파일 시스템에 로그를 쓸 수는 **sysadmin** 고정된 서버 역할입니다. 작업 소유자의 구성원이 아닙니다. 하는 경우는 **sysadmin** 역할과 프록시 계정을 설정 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 프록시 계정의 자격 증명을 사용 하 여 파일 시스템에 로그에 쓸 수 있습니다.  
  
 업그레이드 후 **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자는 자신이 소유한 작업에 대한 로그를 더 이상 파일 시스템에 기록할 수 없습니다. 대신 이러한 사용자는 **msdb** 데이터베이스의 테이블에 로그를 기록하는 옵션을 선택할 수 있습니다. **sysadmin** 역할의 멤버는 계속 파일 시스템에 로그를 기록할 수 있습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 업그레이드 후 **sysadmin** 역할의 멤버가 아닌 사용자가 소유하는 작업은 계속 실행될 수 있지만 로그는 생성되지 않습니다. 테이블에 작업 단계를 기록하려면 **sysadmin** 역할의 멤버가 아닌 사용자가 수동으로 해당 작업을 업데이트해야 합니다.  
  
 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "작업 만들기", "작업 단계 만들기" 및 "다중 작업 단계 처리"를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 에이전트 업그레이드 문제](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  