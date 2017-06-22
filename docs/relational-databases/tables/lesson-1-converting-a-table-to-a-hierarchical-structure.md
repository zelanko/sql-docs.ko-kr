---
title: "1단원: 테이블을 계층 구조로 변환 | Microsoft 문서"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- HierarchyID
ms.assetid: 5ee6f19a-6dd7-4730-a91c-bbed1bd77e0b
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e72d61437876a0fd7c151d9511281860910eb384
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-1-converting-a-table-to-a-hierarchical-structure"></a>1단원: 테이블을 계층 구조로 변환
자체 조인을 사용하여 계층 관계를 나타내는 테이블을 보유하고 있는 경우 이 단원의 내용을 참조하여 해당 테이블을 계층 구조로 변환할 수 있습니다. 이 표현을 **hierarchyid**를 사용하는 표현으로 마이그레이션하는 작업은 비교적 쉽습니다. 마이그레이션하면 간단하고 이해하기 쉬운 계층적 표현이 완성되며 효율적인 쿼리를 위해 여러 가지 방법으로 인덱싱할 수 있습니다.  
  
이 단원에서는 기존 테이블을 검토하고, **hierarchyid** 열이 포함된 새 테이블을 만들고, 원본 테이블의 데이터로 이 테이블을 채운 다음 인덱싱 방법 3가지를 보여 줍니다. 이 단원에서는 다음 항목을 다룹니다.  
  
-   [Employee 테이블의 현재 구조 검사](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
-   [기존 계층적 데이터로 테이블 채우기](../../relational-databases/tables/lesson-1-2-populating-a-table-with-existing-hierarchical-data.md)  
  
-   [NewOrg 테이블 최적화](../../relational-databases/tables/lesson-1-3-optimizing-the-neworg-table.md)  
  
-   [요약: 테이블을 계층 구조로 변환](../../relational-databases/tables/lesson-1-4-summary-converting-a-table-to-a-hierarchical-structure.md)  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 단원에는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스가 필요합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[Employee 테이블의 현재 구조 검사](../../relational-databases/tables/lesson-1-1-examining-the-current-structure-of-the-employee-table.md)  
  
## <a name="next-lesson"></a>다음 단원  
[2단원: 계층적 테이블의 데이터 만들기 및 관리](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
  
  
  

