---
title: MSSQLSERVER_21892 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18916e8287841015727c37ed8833fbc29b1e6ba2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183427"
---
# <a name="mssqlserver21892"></a>MSSQLSERVER_21892
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21892|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum21892|  
|메시지 텍스트|멤버 복제본의 서버 이름에 대해 가상 네트워크 이름 '%s'과(와) 연관된 가용성 그룹 주 복제본에서 sys.availability_replicas를 쿼리할 수 없습니다. 오류 = %d, 오류 메시지 = %s.',|  
  
## <a name="explanation"></a>설명  
 `sp_validate_replica_hosts_as_publishers`는 리디렉션된 게시자와 연관된 가용성 그룹의 현재 주 복제본을 쿼리하여 멤버 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 확인합니다.  이 쿼리에 실패하면 오류 21892가 반환됩니다.  
  
 `sp_validate_replica_hosts_as_publishers`는 일반적으로 임시 연결된 서버를 처음 사용할 때 수행되므로 연결 문제가 있을 경우 가장 먼저 `sp_validate_replica_hosts_as_publishers`에서 연결 문제가 나타날 가능성이 높습니다. `sp_validate_redirected_publisher`와 달리 `sp_validate_replica_hosts_as_publishers`에서 사용하는 연결된 서버는 항상 가용성 그룹 복제본 호스트에 연결할 때 호출자의 자격 증명을 사용합니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 저장 프로시저는 모든 복제본에서 유효한 로그인을 사용하여 실행해야 합니다. 이 로그인에 충분한 권한이 있어야만 가용성 그룹 메타데이터 테이블 및 게시자 데이터베이스 복제본에 있는 구독 메타데이터 테이블을 쿼리할 수 있습니다.  
  
 참조된 원래 오류를 검토하여 실패 원인을 파악하고 적절한 수정 동작을 수행하십시오.  
  
  
