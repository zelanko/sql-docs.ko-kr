---
title: MSSQLSERVER_7933 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7933 (Database Engine error)
ms.assetid: 722bd2c6-0fb9-4838-954a-439744c6ac4b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be3d21665d41fe7748e6a3a4d070f4001ca306a8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201053"
---
# <a name="mssqlserver7933"></a>MSSQLSERVER_7933
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7933|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_FS_ORPHANED_ROWSET_DIRECTORY|  
|메시지 텍스트|테이블 오류: 파티션에 대한 Filestream 디렉터리 ID F_ID이(가) 있지만 해당 파티션이 데이터베이스에 없습니다.|  
  
## <a name="explanation"></a>설명  
 DBCC CHECKDB를 실행하는 동안 FILESTREAM 데이터 공간에서 행 집합 디렉터리를 찾았지만 해당 파티션이 데이터베이스에 없습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
 하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 응용 프로그램 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
 데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인하세요. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하십시오.  
  
 마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하세요.  
  
### <a name="run-dbcc-checkdb"></a>DBCC CHECKDB 실행  
 이 오류에는 이 작업을 적용할 수 없습니다. 이 오류는 자동으로 복구할 수 없습니다. 백업에서 데이터베이스를 복원할 수 없으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS(고객 서비스 지원 센터)에 문의하십시오.  
  
  
