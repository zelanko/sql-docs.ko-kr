---
title: MSSQLSERVER_8992 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 845314b7810b535697a661538622f21054ce400c
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37424852"
---
# <a name="mssqlserver8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>설명  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|8992|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC3_CHECK_CATALOG|  
|메시지 텍스트|카탈로그 검사 메시지 ERROR 수준 LEVEL 상태 STATE: MESSAGE을(를) 확인하십시오.|  
  
## <a name="explanation"></a>설명  
 DBCC CHECKCATALOG 또는 DBCC CHECKDB에서 지정된 개체에 대한 시스템 메타데이터 테이블 간의 불일치를 발견했습니다. 즉, 오류 메시지에 지정된 개체와 기록된 개체 ID가 일치하지 않습니다.  
  
 이 오류는 시스템 메타데이터의 불일치를 유발하는 방식으로 하나 이상의 시스템 테이블을 수동 업데이트한 경우에 발생할 수 있습니다. 예를 들어 사용자가 **sysobjects** 테이블의 개체를 수동으로 삭제할 때 **sysindexes** 및 **syscolumns** 등의 다른 테이블에 있는 연관된 행을 제거하지 않았을 수 있습니다.  
  
 이 오류는 SQL Server 2000에서 SQL Server 2005 이상 버전으로 업그레이드된 데이터베이스에 대해 DBCC CHECKDB를 실행하는 경우에 발생할 수 있습니다. SQL Server 2000의 경우 DBCC CHECKDB에 DBCC CHECKCATALOG 기능이 포함되지 않으므로 SQL Server 2000에서 데이터베이스에 대해 DBCC CHECKCATALOG를 명시적으로 실행하지 않는 한 이 오류는 업그레이드 이전에 발견되지 않습니다.  
  
 오류 8992와 함께 다음과 같은 오류가 표시될 수 있습니다.  
  
 메시지 3851 - 시스템 테이블 sys.%ls%ls에서 잘못된 행(%ls)을 찾았습니다.  
  
 메시지 3852 - sys.%ls%ls의 행(%ls)과 대응하는 행(%ls)이 sys.%ls%ls에 없습니다.  
  
 3853 - sys.%ls%ls의 행(%ls)의 특성(%ls)과 대응하는 행(%ls)이 sys.%ls%ls에 없습니다.  
  
 3854 - sys.%ls%ls의 행(%ls)의 특성(%ls)과 대응하는 행(%ls)이 sys.%ls%ls에 있으나 적합하지 않습니다.  
  
 3855 - 특성(%ls)이 행(%ls)이 없는 상태로 sys.%ls%ls에 존재합니다.  
  
 3856 - sys.%ls%ls의 행(%ls)에 있어서는 안 되는 특성(%ls)이 있습니다.  
  
 3857 - sys.%ls%ls의 행(%ls)에 필요한 특성(%ls)이 없습니다.  
  
 3858 - sys.%ls%ls의 행(%ls)의 특성(%ls)에 잘못된 값이 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
  
### <a name="drop-and-re-create-the-specified-object"></a>지정된 개체 삭제 및 다시 만들기  
 가능한 경우 지정된 개체를 삭제하고 다시 만드십시오. 예를 들어 개체가 저장 프로시저 또는 사용자 정의 형식인 경우 해당 개체를 다시 만들면 이 문제가 해결될 수 있습니다.  
  
### <a name="restore-from-backup"></a>백업에서 복원  
 하드웨어 관련 문제가 아니면 정상적인 백업(있는 경우)을 사용하여 데이터베이스를 복원하세요. 이 동작은 백업에 메타데이터 오류가 포함되지 않은 경우에만 적용할 수 있습니다.  
  
### <a name="export-the-data-to-a-new-database"></a>새 데이터베이스에 데이터 내보내기  
 백업에도 메타데이터 불일치가 있을 경우 새 데이터베이스를 만들어 기존 데이터베이스의 내용을 새 데이터베이스로 내보내야 합니다.  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>DBCC CHECKDB가 이 오류를 복구할 수 없음  
 이 오류를 복구할 수 없습니다.  백업에서 데이터베이스를 복원할 수 없으면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CSS(고객 서비스 지원 센터)에 문의하십시오.  
  
### <a name="do-not-manually-update-system-tables"></a>시스템 테이블 수동 업데이트 금지  
 시스템 테이블을 수동으로 업데이트하지 마십시오. SQL Server는 시스템 데이터베이스에 대한 수동 변경을 지원하지 않습니다. SQL Server 데이터베이스에서 시스템 테이블을 업데이트할 경우 두 가지 이벤트(이벤트 ID 17659와 이벤트 ID 3859)가 기록됩니다. 자세한 내용은 기술 자료 문서 2688307, "SQL Server 데이터베이스의 시스템 테이블을 업데이트할 경우 이벤트 ID 17659와 이벤트 ID 3859가 기록됨"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 데이터베이스의 시스템 테이블을 업데이트할 경우 이벤트 ID 17659와 이벤트 ID 3859가 기록됨](http://support.microsoft.com/kb/2688307/EN-US)  
  
  
