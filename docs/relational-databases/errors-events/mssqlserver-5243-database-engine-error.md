---
title: MSSQLSERVER_5243 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 19fd1351963a578d83e8cf67a48c6f97dcd96afe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078866"
---
# <a name="mssqlserver5243"></a>MSSQLSERVER_5243
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|5243|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름||  
|메시지 텍스트|내부 작업을 수행하는 중 불일치가 감지되었습니다. 기술 지원 서비스에 문의하십시오. 참조 번호는 %ld입니다.|  
  
## <a name="explanation"></a>설명  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 메모리 내 스토리지 엔진 구조에서 구조적 불일치를 감지했습니다.  
  
## <a name="user-action"></a>사용자 동작  
하드웨어 오류를 찾습니다. 하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. Windows 시스템 및 애플리케이션 로그와 SQL Server 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하세요. 로그에 하드웨어 관련 문제가 있으면 모두 해결합니다.

데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인합니다. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하세요.

마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.

백업에서 복원. 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원합니다.

DBCC CHECKDB 실행. 정상적인 백업이 없으면 REPAIR 절 없이 DBCC CHECKDB를 실행하여 손상된 정도를 확인합니다. DBCC CHECKDB 실행 시 REPAIR 절을 사용하라는 메시지가 나타나면 적합한 REPAIR 절을 사용하여 DBCC CHECKDB를 실행하고 손상을 복구하십시오.

> **경고 태그는 지원되지 않습니다.**
> **tr 태그는 지원되지 않습니다.**
> **tr 태그는 지원되지 않습니다.**

REPAIR 절 중 하나를 사용하여 DBCC CHECKDB를 실행해도 문제가 해결되지 않으면 주 지원 공급자에게 문의하세요.
  
## <a name="see-also"></a>참고 항목  
[DBCC CHECKDB&#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[데이터베이스 파일 및 파일 그룹](~/relational-databases/databases/database-files-and-filegroups.md)  
  
