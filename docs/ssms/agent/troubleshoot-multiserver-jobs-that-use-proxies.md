---
title: "프록시를 사용하는 다중 서버 작업 문제 해결 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6a02ace1fe1ba285bc340b9dca87112325f97210
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>프록시를 사용하는 다중 서버 작업 문제 해결
프록시와 연관된 단계가 있는 분산된 작업은 대상 서버의 프록시 계정 컨텍스트 하에서 실행됩니다. 마스터 서버에서 다운로드할 때 프록시 계정을 사용하는 작업 단계가 실패한 경우 **msdb** 데이터베이스 **sysdownloadlist** 테이블의 **error_message** 열에서 다음 오류 메시지를 확인합니다.  
  
-   "작업 단계에 프록시 계정이 필요하지만 일치하는 프록시를 대상 서버에서 사용할 수 없습니다."  
  
    이 오류를 해결하려면 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>**\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** 레지스트리 하위 키를 **1(true)**로 설정합니다. 기본적으로 이 하위 키는 **0** (**false**)으로 설정됩니다. **MSSQL.**\<*n*>의 값은 인스턴스 이름입니다(예: **MSSQL.1** 또는 **MSSQL.3**).  
  
-   "프록시를 찾을 수 없습니다."  
  
    이 오류를 해결하려면 프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 확인합니다.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>관련 항목:  
[다중 서버 환경 만들기](../../ssms/agent/create-a-multiserver-environment.md)  
  

