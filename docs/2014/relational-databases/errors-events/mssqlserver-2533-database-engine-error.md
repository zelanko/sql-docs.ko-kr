---
title: MSSQLSERVER_2533 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2533 (Database Engine error)
ms.assetid: 0418352c-0ab2-4dc7-b8b9-5c3bad94560c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b1882c04d4aacd76b59cb952781205edac84012
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914821"
---
# <a name="mssqlserver2533"></a>MSSQLSERVER_2533
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2533|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_PAGE_WAS_NOT_SEEN|  
|메시지 텍스트|테이블 오류: 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 된 페이지 P_ID, 할당 단위 ID A_ID (type 유형) 표시 되지 않습니다. 페이지가 잘못되었거나 페이지 머리글의 할당 단위 ID가 잘못되었을 수 있습니다.|  
  
## <a name="explanation"></a>설명  
 페이지가 할당 단위 ID *A_ID*에 할당되었지만 이 할당 단위는 페이지 머리글에 없습니다. 헤더에 다른 할당 단위 ID가 있습니다. 페이지 헤더에 있는 할당 단위 ID가 올바른 개체에 대한 것이면 해당 페이지에 MSSQLEngine_2534 오류가 발생할 수 있습니다.  
  
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
>  REPAIR 절을 사용할 경우 DBCC CHECKDB가 데이터에 미치는 영향을 확인하려면 이 문을 실행하기 전에 주 지원 공급자에게 문의하세요.  
  
 REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행해도 문제가 해결되지 않으면 주 지원 공급자에게 문의하세요.  
  
### <a name="results-of-running-repair-options"></a>REPAIR 옵션의 실행 결과  
 REPAIR는 페이지 할당을 취소합니다. 이 페이지가 행 내부 데이터 할당 단위에 속하면 인덱스가 있는 경우 인덱스가 다시 작성됩니다.  
  
> [!CAUTION]  
>  이 복구로 인해 데이터가 손실될 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [MSSQLSERVER_2534](mssqlserver-2534-database-engine-error.md)  
  
  
