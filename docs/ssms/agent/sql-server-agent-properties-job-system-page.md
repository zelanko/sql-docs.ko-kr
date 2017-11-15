---
title: "SQL Server 에이전트 속성(작업 시스템 페이지) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed055e6b7a9c560c0ac05c11f930c49b681de0aa
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-job-system-page"></a>SQL Server 에이전트 속성(작업 시스템 페이지)
이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스의 작업 관리 방법을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**시스템 종료 제한 시간 간격(초)**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트의 종료 전 작업 완료 대기 시간(초)을 지정합니다. 지정한 간격을 초과하여 작업이 실행되는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트가 강제로 작업을 중지합니다.  
  
**비관리자 프록시 계정 사용**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트에 대한 비관리자 프록시 계정을 설정합니다. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] 이상 버전에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**사용자 이름**  
비관리자 프록시 계정에 대한 사용자의 이름을 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**암호**  
비관리자 프록시 계정에 대한 사용자의 암호를 입력합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 이상 버전에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
**도메인**  
비관리자 프록시 계정에 대한 사용자의 도메인을 입력합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에서는 여러 프록시를 지원하므로 이 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 이전 버전의 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]에이전트를 관리할 때만 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[작업 구현](../../ssms/agent/implement-jobs.md)  
  
