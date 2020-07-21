---
title: MSSQLSERVER_2515 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2515 (Database Engine error)
ms.assetid: af93aa29-70c9-4923-90af-aafadb20c1c6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 052606d99f825d50c073f68c078a414df4d69d9e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552128"
---
# <a name="mssqlserver_2515"></a>MSSQLSERVER_2515
    
## <a name="details"></a>세부 정보  
  
|attribute|값|  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|2515|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_DIFF_MAP_OUT_OF_SYNC|  
|메시지 텍스트|페이지 P_ID, 개체 ID O_ID, 인덱스 ID I_ID, 파티션 ID PN_ID, 할당 단위 ID A_ID(TYPE 유형)이(가) 수정되었지만 차등 백업 비트맵에서 수정된 것으로 표시되지 않았습니다.|  
  
## <a name="explanation"></a>설명  
 지정된 페이지에 있는 LSN(로그 시퀀스 번호)은 어느 것이 더 최근 값인지에 관계없이 데이터베이스의 BackupManager에 있는 차등 참조 LSN이나 파일의 파일 제어 블록의 차등 기반 LSN보다 높은 값을 가집니다. 그러나 페이지는 차등 백업 비트맵에서 변경된 것으로 표시되지 않았습니다.  
  
 이 검사는 차등 비트맵에 오류가 없는 경우에만 수행되므로 데이터베이스당 한 페이지만 보고됩니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
 하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 애플리케이션 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
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
 REPAIR를 실행하면 차등 비트맵이 무효화됩니다. 전체 데이터베이스 백업이 수행되기까지 차등 백업을 수행할 수 없습니다. 전체 데이터베이스 백업은 차등 비트맵을 다시 작성하기 위한 기준점이 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)   
 [MSSQLSERVER_2516](mssqlserver-2516-database-engine-error.md)  
  
  
