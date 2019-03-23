---
title: 인덱스 다시 작성 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rebuildindextask.f1
helpviewer_keywords:
- rebuilding indexes
- indexes [Integration Services]
- Rebuild Index task
ms.assetid: 021884dd-e72d-47b2-99e8-b741410509c3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9e89c081c1c543c198a827955ab4865709ead391
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392691"
---
# <a name="rebuild-index-task"></a>인덱스 다시 작성 태스크
  인덱스 다시 작성 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 테이블과 뷰의 인덱스를 다시 작성합니다. 인덱스 관리에 대한 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)을 참조하세요.  
  
 인덱스 다시 작성 태스크를 사용하면 패키지가 단일 데이터베이스나 여러 데이터베이스의 인덱스를 다시 작성할 수 있습니다. 태스크가 단일 데이터베이스의 인덱스만 다시 작성하는 경우 인덱스를 다시 작성할 뷰와 테이블을 선택할 수 있습니다.  
  
 이 태스크는 ALTER INDEX REBUILD 문을 다음 인덱스 다시 작성 옵션과 함께 캡슐화합니다.  
  
-   FILLFACTOR 비율을 지정하거나 원래 FILLFACTOR 수량을 사용합니다.  
  
-   PAD_INDEX = ON을 설정하여 FILLFACTOR로 지정된 사용 가능한 공간을 인덱스의 중간 수준 페이지에 할당할 수 있습니다.  
  
-   SORT_IN_TEMPDB = ON을 설정하여 인덱스를 다시 작성하는 데 사용된 중간 정렬 결과를 tempdb에 저장할 수 있습니다. 중간 정렬 결과를 OFF로 설정하면 인덱스와 동일한 데이터베이스에 결과가 저장됩니다.  
  
-   IGNORE_DUP_KEY = ON을 설정하여 UNIQUE 제약 조건을 위반하는 레코드가 포함된 다중 행 삽입 작업에서 UNIQUE 제약 조건을 위반하지 않는 레코드를 삽입할 수 있습니다.  
  
-   ONLINE = ON을 설정하여 다시 인덱싱하는 동안 기본 테이블에 대한 쿼리 또는 업데이트가 진행될 수 있도록 테이블을 잠그지 않을 수 있습니다.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 사용할 수 있습니다. 버전에서 지원 되는 기능 목록은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조 하세요 [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 ALTER INDEX 문과 인덱스 다시 작성 옵션에 대한 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)를 참조하세요.  
  
> [!IMPORTANT]  
>  태스크에서 실행할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 만드는 데 걸리는 시간은 태스크에서 다시 작성하는 인덱스 수에 비례합니다. 많은 수의 인덱스가 있는 데이터베이스의 모든 테이블과 뷰의 인덱스를 다시 작성하거나 여러 데이터베이스의 인덱스를 다시 작성하도록 태스크를 구성하면 Transact-SQL 문을 생성하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="configuration-of-the-rebuild-index-task"></a>인덱스 다시 작성 태스크 구성  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
 [인덱스 다시 작성 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법에 대한 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
