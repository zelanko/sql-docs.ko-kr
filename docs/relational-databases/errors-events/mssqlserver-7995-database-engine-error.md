---
title: MSSQLSERVER_7995 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7995 (Database Engine error)
ms.assetid: af6d6322-3cba-43d8-be97-e6ef15f8c933
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16f2bebd761898fad44cd19c78c02470420b6d18
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72906554"
---
# <a name="mssqlserver_7995"></a>MSSQLSERVER_7995
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|7995|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC2_SYSTEM_CATALOGS_CORRUPT|  
|메시지 텍스트|데이터베이스 'DBNAME': 시스템 카탈로그의 일관성 오류로 인해 DBCC CHECKNAME 프로세스를 계속 진행할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
DBCC CHECKDB 프로세스는 다음 세 단계로 구성됩니다.  
  
1.  할당을 검사합니다. 이는 DBCC CHECKALLOC을 실행하는 것과 같습니다.  
  
2.  시스템 테이블의 일관성을 검사합니다. 이는 몇몇 필수적인 시스템 기본 테이블에 대해 DBCC CHECKTABLE을 실행하는 것과 같습니다.  
  
3.  데이터베이스 일관성 검사를 완료합니다.  

MSSQLEngine_7995 오류는 2단계에서 발생하며 DBCC CHECKDB에서 명령으로 복구할 수 없거나 REPAIR가 지정되지 않은 오류를 발견했음을 나타냅니다. 검사 중인 시스템 기본 테이블에 데이터베이스의 모든 개체에 대한 메타데이터가 저장되어 있거나 시스템 기본 테이블이 손상되어 DBCC CHECKDB는 3단계로 계속 진행할 수 없습니다.  
  
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
> REPAIR 절을 사용할 경우 DBCC CHECKDB가 데이터에 미치는 영향을 확인하려면 이 문을 실행하기 전에 주 지원 공급자에게 문의하세요.  
  
REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행해도 문제가 해결되지 않으면 주 지원 공급자에게 문의하세요.  
  
### <a name="results-of-running-repair-options"></a>REPAIR 옵션의 실행 결과  
오류 목록을 검사하여 REPAIR가 각각에 대해 수행할 작업을 확인하십시오.  
  
