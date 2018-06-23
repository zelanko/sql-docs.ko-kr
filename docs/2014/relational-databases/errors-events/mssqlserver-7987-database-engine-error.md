---
title: MSSQLSERVER_7987 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 7987 (Database Engine error)
ms.assetid: 314aebf1-6cdf-488d-a274-ce967fadb57b
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a10045daa8d595da3487c5b3d3abdef04c051bab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36184945"
---
# <a name="mssqlserver7987"></a>MSSQLSERVER_7987
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7987|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_PRE_CHECKS_CHAIN_LINKAGE_MISMATCH|  
|메시지 텍스트|시스템 테이블 사전 검사: 개체 ID O_ID의 체인 연결이 일치하지 않습니다. P_ID1->next = P_ID2인데 P_ID2->prev = P_ID3입니다. 오류로 인해 검사 문이 종료됩니다.|  
  
## <a name="explanation"></a>설명  
 DBCC CHECKDB의 첫 번째 단계는 중요 시스템 테이블의 데이터 페이지에 대해 기본 검사를 수행하는 것입니다. 오류가 발견되는 경우 이를 복구할 수 없으므로 DBCC CHECKDB가 즉시 종료됩니다.  
  
 *P_ID1* 페이지의 다음 페이지 포인터가 *P_ID2* 페이지를 가리킵니다. 그러나 *P_ID2* 페이지의 이전 페이지 포인터는 *P_ID3* 페이지를 가리키고 *P_ID1* 페이지로 돌아갈 수 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
 하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 응용 프로그램 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
 데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인하세요. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하십시오.  
  
 마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하세요.  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB 실행  
 이 오류에는 이 작업을 적용할 수 없습니다. 이 오류는 자동으로 복구할 수 없습니다. 백업에서 데이터베이스를 복원할 수 없으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS(고객 서비스 지원 센터)에 문의하십시오.  
  
  