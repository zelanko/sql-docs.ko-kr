---
title: 프록시를 사용하는 다중 서버 작업 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47e3c3991bd4732d542bf1ce79e83000e738ff77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245420"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>프록시를 사용하는 다중 서버 작업 문제 해결
  프록시와 연관된 단계가 있는 분산된 작업은 대상 서버의 프록시 계정 컨텍스트 하에서 실행됩니다. 마스터 서버에서 다운로드할 때 프록시 계정을 사용하는 작업 단계가 실패한 경우 **msdb** 데이터베이스 **sysdownloadlist** 테이블의 **error_message** 열에서 다음 오류 메시지를 확인합니다.  
  
-   "작업 단계에 프록시 계정이 필요하지만 일치하는 프록시를 대상 서버에서 사용할 수 없습니다."  
  
     이 오류를 해결 하려면 **\ HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\MSSQL.** 를 설정 하십시오. >**\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** _ \<n_\SQLServerAgent\AllowDownloadedJobsToMatchProxyName 레지스트리 하위 키를 **1 (true)로 설정**합니다. 기본적으로이 하위 키는 **0** (`false`)으로 설정 됩니다. MSSQL의 값입니다 **.** \< *n*>은 인스턴스 이름입니다. 예를 들어 **mssql. 1** 또는 **mssql. 3**입니다.  
  
-   "프록시를 찾을 수 없습니다."  
  
     이 오류를 해결하려면 프록시 계정이 작업 단계가 실행되는 마스터 서버 프록시 계정과 동일한 이름을 가진 대상 서버에 있는지 확인합니다.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [다중 서버 환경 만들기](create-a-multiserver-environment.md)  
  
  
