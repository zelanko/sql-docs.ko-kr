---
title: 메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9b9e442fb97245d32c398602cdfd727de8239cb8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53352426"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항
  이외에 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md), 다음은 메모리 내 OLTP를 사용 하기 위한 요구 사항:  
  
-   64비트 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise, Developer 또는 Evaluation Edition이 필요합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 메모리 최적화 테이블에 데이터를 저장하기에 충분한 메모리가 필요합니다. 행 버전을 지원하기 위해서는 메모리 최적화 테이블 및 인덱스의 예상 크기의 두 배에 해당하는 메모리 양을 제공해야 합니다. 하지만 실제로 필요한 메모리 양은 작업에 따라 다릅니다. 메모리 사용량을 모니터링하고 필요한 대로 조정해야 합니다. 메모리 최적화 테이블의 데이터 크기는 풀을 기준으로 허용된 비율을 초과할 수 없습니다. 메모리 최적화 테이블의 크기를 검색 하려면 참조 [sys.dm_db_xtp_table_memory_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)합니다.  
  
     데이터베이스에 디스크 기반 테이블이 있는 경우 버퍼 풀 및 해당 테이블에 대한 쿼리 처리에 충분한 메모리를 제공해야 합니다.  
  
     메모리 내 OLTP 애플리케이션에 필요한 메모리 양을 알고 있어야 합니다. 자세한 내용은 [메모리 액세스에 최적화된 테이블에 필요한 메모리 예측](memory-optimized-tables.md) 을 참조하세요.  
  
-   지속형 메모리 최적화 테이블 크기의 2배에 해당하는 여유 디스크 공간  
  
-   메모리 내 OLTP를 사용하려면 프로세서에서 **cmpxchg16b** 명령어를 지원해야 합니다. 최신 64비트 프로세서는 **cmpxchg16b**를 지원합니다.  
  
     VM 호스트 애플리케이션을 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 이전 프로세서로 인한 오류가 표시되면 **cmpxchg16b**를 허용하도록 애플리케이션의 구성 옵션이 설정되어 있는지 확인하십시오. 설정되어 있지 않은 경우 구성 옵션을 설정할 필요 없이 **cmpxchg16b** 를 지원하는 Hyper-V를 사용할 수 있습니다.  
  
-   메모리 내 OLTP를 설치하려면 **를 설치할 때** 데이터베이스 엔진 서비스 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 선택합니다.  
  
     보고서 생성을 설치 하려면 ([Determining if 테이블 또는 저장 프로시저를 이식 해야 메모리 내 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 및 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (통해 메모리 내 OLTP를 관리 하 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 개체 탐색기)를 선택 **관리 도구-기본** 나 **관리 도구-고급** 설치 하는 경우 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]합니다.  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>[!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 사용에 관한 중요 사항  
  
-   데이터베이스에 있는 모든 영구 테이블의 총 메모리 내 크기는 250GB를 초과할 수 없습니다. 자세한 내용은 [메모리 최적화 테이블에 대 한 내구성](durability-for-memory-optimized-tables.md)합니다.  
  
-   이 버전의 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]는 소켓이 2 - 4개이고 코어가 60개 미만인 시스템에서 최적으로 수행되도록 설계되었습니다.  
  
-   검사점 파일을 수동으로 삭제해서는 안 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 불필요한 검사점 파일에서 가비지 수집을 자동으로 수행합니다. 자세한 내용은 참조의 데이터 및 델타 파일 병합 [메모리 최적화 테이블에 대 한 내구성](durability-for-memory-optimized-tables.md)합니다.  
  
-   메모리 내 OLTP의 이 첫 번째 릴리스에서([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서) 메모리 최적화 파일 그룹을 제거하는 유일한 방법은 데이터베이스를 삭제하는 것입니다.  
  
-   삭제하려는 행의 범위에 영향을 주는 동시 삽입 또는 업데이트 작업이 있는 상태에서 큰 행 일괄 처리를 삭제하려고 하면 삭제가 실패합니다. 문제를 해결하려면 삭제하기 전에 삽입 또는 업데이트 작업을 중지합니다. 또는 트랜잭션을 더 작은 트랜잭션으로 구성할 수 있습니다. 그러면 동시 작업에 의해 트랜잭션이 중단될 가능성이 더 낮아집니다. 메모리 최적화 테이블에서의 모든 쓰기 작업과 마찬가지로 재시도 논리([Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md))를 사용합니다.  
  
-   메모리 최적화 테이블로 하나 이상의 데이터베이스를 만들 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 즉시 파일 초기화([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정에 SE_MANAGE_VOLUME_NAME 사용자 권한 부여)를 사용하도록 설정해야 합니다. 즉시 파일 초기화를 사용하지 않을 경우 메모리 최적화 스토리지 파일(데이터 및 델타 파일)이 생성될 때 초기화되므로 작업 성능이 저하될 수 있습니다. 즉시 파일 초기화에 대한 자세한 내용은 [데이터베이스 파일 초기화](../databases/database-instant-file-initialization.md)를 참조하세요. 즉시 파일 초기화를 사용하도록 설정하는 방법은 [즉시 파일 초기화를 사용하도록 설정하는 방법과 이유](https://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)를 참조하세요.  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 피드백 환영  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 콘텐츠를 개선 하기 위해 귀하의 의견을 환영 합니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page)에 대한 비즈니스 규칙의 예를 보여 줍니다.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
