---
title: "MSSQLSERVER_9955 | Microsoft 문서"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8c4d27af44152bb9b9816dbcdb0af7c75ea2f4db
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9955"></a>MSSQLSERVER_9955
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|9955|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|FTXT2_MSSEARCHACCESSDENY|  
|메시지 텍스트|SQL Server에서 전체 텍스트 필터 데몬(Windows 오류: %d)과 통신하는 명명된 파이프 '%ls'을(를) 만들지 못했습니다. 필터 데몬 호스트 프로세스에 대한 명명된 파이프가 이미 있거나, 시스템 리소스 공간이 부족하거나, 필터 데몬 계정 그룹에 대한 SID(보안 ID)를 조회하지 못했습니다. 이 오류를 해결하려면 실행 중인 전체 텍스트 필터 데몬 프로세스를 종료하고, 필요한 경우 전체 텍스트 데몬 시작 관리자 서비스 계정을 다시 구성하십시오.|  
  
## <a name="explanation"></a>설명  
이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 필터 데몬과 통신하는 명명된 파이프를 만들지 못한 경우에 발생합니다. 필터 데몬 호스트 프로세스에 대한 명명된 파이프가 이미 있거나, 시스템 리소스 공간이 부족하거나, 필터 데몬 계정 그룹에 대한 SID(보안 ID)를 조회하지 못했습니다.  
  
## <a name="user-action"></a>사용자 동작  
이 오류를 해결하려면 실행 중인 전체 텍스트 필터 데몬 프로세스를 종료하고, 필요한 경우 SQL Server 구성 관리자를 사용하여 전체 텍스트 데몬 호스트 계정을 다시 구성하십시오.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server 구성 관리자](~/relational-databases/sql-server-configuration-manager.md)  
[전체 텍스트 필터 데몬 시작 관리자 서비스 계정 설정](~/relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)  
[전체 텍스트 검색](~/relational-databases/search/full-text-search.md)  
  

