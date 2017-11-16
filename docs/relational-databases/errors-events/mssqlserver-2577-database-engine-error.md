---
title: "MSSQLSERVER_2577 | Microsoft 문서"
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
- 2577 (Database Engine error)
ms.assetid: f53256a2-2fb0-47fd-9ed9-c45389104145
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1244598f5e9b836eb3d3aefa1bd13011d527bfdc
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2577"></a>MSSQLSERVER_2577
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2577|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_IAM_CHAIN_SEQUENCE_OUT_OF_ORDER|  
|메시지 텍스트|개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)의 IAM(Index Allocation Map) 체인에서 체인 시퀀스 번호가 잘못되었습니다. 시퀀스 번호 SEQUENCE1의 페이지 P_ID1이(가) 시퀀스 번호 SEQUENCE2의 페이지 P_ID2을(를) 가리킵니다.|  
  
## <a name="explanation"></a>설명  
모든 IAM(Index Allocation Map) 페이지에는 시퀀스 번호가 있습니다. 시퀀스 번호는 IAM 체인 내에서의 IAM 페이지 위치이며 각 IAM 페이지에 대해 시퀀스 번호가 1씩 증가하는 것이 규칙입니다. IAM 페이지 *P_ID2*의 시퀀스 번호가 이 규칙에 어긋납니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 응용 프로그램 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인하세요. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하십시오.  
  
마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하세요.  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB 실행  
정상적인 백업이 없으면 REPAIR 절 없이 DBCC CHECKDB를 실행하여 손상된 정도를 확인하십시오. DBCC CHECKDB 실행 시 REPAIR 절을 사용하라는 메시지가 나타나면 적합한 REPAIR 절을 사용하여 DBCC CHECKDB를 실행하고 손상을 복구하십시오.  
  
> [!CAUTION]  
> REPAIR 절을 사용할 경우 DBCC CHECKDB가 데이터에 미치는 영향을 확인하려면 이 문을 실행하기 전에 주 지원 공급자에게 문의하세요.  
  
REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행해도 문제가 해결되지 않으면 주 지원 공급자에게 문의하세요.  
  
### <a name="results-of-running-repair-options"></a>REPAIR 옵션의 실행 결과  
REPAIR을 실행하여 IAM 체인을 다시 작성합니다. REPAIR는 먼저 기존 IAM 체인을 반으로 나눕니다. 체인의 첫 번째 절반은 IAM 페이지 *P_ID1*로 끝납니다. *P_ID1* 페이지의 다음 페이지 포인터는 (0:0)으로 설정됩니다. 체인의 두 번째 절반은 IAM 페이지 *P_ID2*로 시작됩니다. *P_ID2* 페이지의 이전 페이지 포인터는 (0:0)으로 설정됩니다.  
  
그런 다음 REPAIR에서 이 둘을 연결하고 IAM 체인의 시퀀스 번호를 다시 생성합니다. 복구할 수 없는 IAM 페이지는 할당이 취소됩니다.  
  
> [!CAUTION]  
> 이 복구로 인해 데이터가 손실될 수 있습니다.  
  

