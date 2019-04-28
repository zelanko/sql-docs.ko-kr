---
title: MSSQLSERVER_2576 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2576 (Database Engine error)
ms.assetid: b727cc2f-c76c-46f8-bbbe-5e7a05a6eabf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26e5e3cbf02191edd84b26505120ee2470e65d24
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62868937"
---
# <a name="mssqlserver2576"></a>MSSQLSERVER_2576
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2576|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_IAM_PARENT_PAGE_WAS_NOT_SEEN|  
|메시지 텍스트|IAM(Index Allocation Map) 페이지 P_ID1이(가) 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)에 있는 IAM 페이지 P_ID2의 이전 포인터에 의해 지정되었으나 검색 시 감지되지 않았습니다.|  
  
## <a name="explanation"></a>설명  
페이지에 대한 참조가 IAM 체인의 다른 IAM 페이지에 이전 페이지 링크로 존재하지만 이 IAM(Index Allocation Map) 페이지 또는 메타데이터 항목을 찾을 수 없습니다. *P_ID1* 페이지가 (0:0)이면 IAM 페이지 *P_ID2*는 IAM 체인의 시작이며 IAM 체인에 대한 메타데이터 항목이 누락되었습니다.  
  
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
REPAIR는 *P_ID2* 페이지와 관련된 IAM 체인을 다시 작성합니다. 체인을 다시 작성하기 위해 체인에서 페이지를 제거하거나 메타데이터가 손상된 경우 전체 체인을 제거해야 할 수 있습니다.  
  
> [!CAUTION]  
> 이 복구로 인해 데이터가 손실될 수 있습니다.  
  
