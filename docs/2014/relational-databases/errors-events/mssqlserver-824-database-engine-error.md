---
title: MSSQLSERVER_824 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de65488eed3e0e93f706cfba619fe1a5608d328
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407680"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|824|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|B_HARDSSERR|  
|메시지 텍스트|SQL Server에서 일관성 기반의 논리적인 I/O 오류가 검색되었습니다. %ls. 파일 '%ls'의 오프셋 %#016I64x에서 데이터베이스 ID %d에 있는 페이지 %S_PGID의 %S_MSG 중 이 오류가 발생했습니다.  자세한 내용은 SQL Server 오류 로그 또는 시스템 이벤트 로그의 추가 메시지에서 확인할 수 있습니다.|  
  
## <a name="explanation"></a>설명  
 이 오류는 Windows가 디스크에서 페이지를 성공적으로 읽었음을 보고하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 해당 페이지에서 잘못된 내용을 발견했음을 나타냅니다. 이 오류는 Windows에서 오류를 감지하지 못한다는 점만 제외하면 오류 823과 비슷합니다. 일반적으로 이 오류는 디스크 드라이브 실패, 디스크 펌웨어 문제, 잘못된 장치 드라이버 등 I/O 하위 시스템의 문제를 나타냅니다. I/O 오류에 대한 자세한 내용은 [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370)(Microsoft SQL Server I/O 기본 사항, 2장)를 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="look-for-hardware-failure"></a>하드웨어 오류 찾기  
 하드웨어 진단을 실행하여 문제가 있으면 이를 해결하십시오. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 시스템 및 응용 프로그램 로그와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그도 검토하여 해당 오류가 하드웨어 오류로 인해 발생했는지 확인하십시오. 로그에 하드웨어 관련 문제가 포함되어 있으면 이를 해결하십시오.  
  
 데이터 손상 문제가 지속되면 다른 하드웨어 구성 요소로 교체하여 문제를 해결하십시오. 시스템의 디스크 컨트롤러에 쓰기 캐시가 설정되어 있지 않은지 확인하세요. 쓰기 캐시가 문제가 된다고 생각되면 하드웨어 공급업체에 문의하십시오.  
  
 마지막으로 새 하드웨어 시스템으로 교체하는 것이 유용할 수도 있습니다. 여기에는 디스크 드라이브를 다시 포맷하고 운영 체제를 다시 설치하는 작업도 포함됩니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하십시오.  
  
 PAGE_VERIFY CHECKSUM 옵션을 사용하도록 데이터베이스를 변경해 보십시오. PAGE_VERIFY에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](../backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
