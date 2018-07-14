---
title: 대량 가져오기의 최소 로깅을 위한 필수 조건 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 956b1af15c2356225d9429bccad6a8d1f4f515e2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172804"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Prerequisites for Minimal Logging in Bulk Import
  전체 복구 모델을 사용하는 데이터베이스의 경우 대량 가져오기로 수행되는 모든 행 삽입 작업이 트랜잭션 로그에 기록됩니다. 전체 복구 모델을 사용할 경우 많은 양의 데이터를 가져오면 트랜잭션 로그가 빨리 채워질 수 있습니다. 이와 달리 단순 복구 모델 또는 대량 로그 복구 모델에서 대량 가져오기 작업의 로깅을 최소화하면 대량 가져오기 작업에 의해 로그 공간이 채워질 가능성이 줄어듭니다. 또한 최소 로깅은 전체 로깅보다 효율적입니다.  
  
> [!NOTE]  
>  대량 로그 복구 모델은 대규모의 대량 작업 중에 전체 복구 모델을 임시로 대체하기 위해 고안된 것입니다.  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>대량 가져오기 작업의 최소 로깅을 위한 테이블 요구 사항  
 최소 로깅에서 대상 테이블은 다음 조건을 충족해야 합니다.  
  
-   테이블이 복제되고 있지 않아야 합니다.  
  
-   테이블 잠금이 지정되어야 합니다(TABLOCK 사용).  
  
    > [!NOTE]  
    >  대량 가져오기 작업을 최소 로깅으로 수행하는 동안 데이터 삽입은 트랜잭션 로그에 기록되지 않지만 새 익스텐트를 테이블에 할당할 때마다 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 익스텐트 할당을 기록합니다.  
  
-   메모리 최적화 테이블이 아닙니다.  
  
 테이블에 대한 최소 로깅의 발생 여부는 다음과 같이 테이블의 인덱싱 여부에 따라 달라지고, 테이블이 인덱싱되는 경우 테이블이 비어 있는지 여부에 따라 달라집니다.  
  
-   테이블에 인덱스가 없는 경우 데이터 페이지가 최소 로깅됩니다.  
  
-   테이블에 클러스터형 인덱스는 없지만 하나 이상의 비클러스터형 인덱스가 있는 경우 데이터 페이지는 항상 최소 로깅됩니다. 그러나 인덱스 페이지 로깅 방법은 다음과 같이 테이블이 비어 있는지 여부에 따라 달라집니다.  
  
    -   테이블이 비어 있는 경우 인덱스 페이지가 최소 로깅됩니다.  
  
    -   테이블이 비어 있지 않은 경우 인덱스 페이지가 모두 로깅됩니다.  
  
        > [!NOTE]  
        >  빈 테이블로 시작하여 데이터 대량 가져오기를 다중 일괄 처리로 수행하는 경우 첫 번째 일괄 처리에서는 인덱스 및 데이터 페이지가 최소 로깅되지만 두 번째 일괄 처리부터는 데이터 페이지만 최소 로깅됩니다.  
  
-   테이블에 클러스터형 인덱스가 있고 비어 있는 경우 데이터 및 인덱스 페이지가 모두 최소 로깅됩니다. 이와 달리 테이블에 클러스터형 인덱스가 있고 비어 있지 않은 경우 데이터 페이지와 인덱스 페이지는 복구 모델에 관계없이 모두 로깅됩니다.  
  
    > [!NOTE]  
    >  빈 테이블로 시작하여 데이터 대량 가져오기를 일괄 처리로 수행하는 경우 첫 번째 일괄 처리에서는 인덱스 및 데이터 페이지가 최소 로깅되지만 두 번째 일괄 처리부터는 데이터 페이지만 대량으로 로깅됩니다.  
  
> [!NOTE]  
>  트랜잭션 복제를 사용하는 경우 대량 로그 복구 모델에서도 BULK INSERT 작업이 모두 기록됩니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  

  
## <a name="see-also"></a>관련 항목  
 [복구 모델&#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET&#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [테이블 힌트&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
