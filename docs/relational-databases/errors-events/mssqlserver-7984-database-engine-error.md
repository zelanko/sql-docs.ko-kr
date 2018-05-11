---
title: MSSQLSERVER_7984 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7984 (Database Engine error)
ms.assetid: e3192f56-e4e2-41da-b132-65f1e7540b1a
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7e16bd11f0834a44ecdc11e46f61bf8483ca413b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver7984"></a>MSSQLSERVER_7984
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7984|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_PRE_CHECKS_BAD_PAGE_TYPE|  
|메시지 텍스트|시스템 테이블 사전 검사: 개체 ID가 O_ID입니다. 페이지 P_ID에 예기치 않은 페이지 유형 PAGETYPE이(가) 있습니다. 오류로 인해 검사 문이 종료됩니다.|  
  
## <a name="explanation"></a>설명  
지정된 개체의 데이터 수준에서 페이지 유형이 DATA_PAGE가 아닌 페이지를 발견했습니다. 이 오류는 DBCC CHECKDB 명령의 첫 번째 단계 검사 중에 발생합니다. 이 단계에서 DBCC CHECKDB는 중요 시스템 기본 테이블의 데이터 페이지에 대한 기본 검사를 수행합니다.  
  
> [!NOTE]  
> 시스템 테이블에서 발견된 오류는 복구할 수 없으므로 DBCC CHECKDB 명령이 즉시 종료됩니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 응용 프로그램 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인하세요. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하십시오.  
  
마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하세요.  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB 실행  
이 오류에는 이 작업을 적용할 수 없습니다. 이 오류는 자동으로 복구할 수 없습니다. 백업에서 데이터베이스를 복원할 수 없으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS(고객 서비스 지원 센터)에 문의하십시오.  
  
