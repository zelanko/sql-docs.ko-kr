---
title: CHECK 제약 조건 대화 상자(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraint
ms.assetid: ad0bbf7f-b0de-406a-bd0a-cb779816b101
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d41cc9f3b52c0c5e70ead6b93c0b929ef521f673
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067459"
---
# <a name="check-constraint-dialog-box-visual-database-tools"></a>CHECK 제약 조건 대화 상자(Visual Database Tools)
  이 대화 상자는 테이블 디자이너에서 테이블 정의 표를 마우스 오른쪽 단추로 클릭한 다음 **CHECK 제약 조건**을 클릭하면 나타납니다. 이 대화 상자에는 데이터베이스의 테이블에 연결된 비 UNIQUE 제약 조건에 대한 속성 집합이 포함되어 있습니다. UNIQUE 제약 조건에 적용되는 속성은 **인덱스/키** 대화 상자에 표시됩니다.  
  
> [!NOTE]  
>  테이블이 복제용으로 게시된 경우 Transact-SQL 문 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) 또는 SMO(SQL Server 관리 개체)를 사용하여 스키마를 변경해야 합니다. 테이블 디자이너 또는 데이터베이스 다이어그램 디자이너를 사용하여 스키마를 변경하면 테이블 삭제 및 재생성이 시도됩니다. 게시된 개체를 삭제할 수 없으므로 스키마가 변경되지 않습니다.  
  
## <a name="options"></a>변수  
 **선택한 CHECK 제약 조건**  
 사용할 수 있는 CHECK 제약 조건을 나열합니다. 제약 조건의 속성을 보려면 목록에서 제약 조건을 선택합니다.  
  
 **추가**  
 선택한 데이터베이스 테이블에 대한 새 제약 조건을 만들고 제약 조건에 기본 이름과 기타 값을 제공합니다. 제약 조건을 유효하게 만들려면 제약 조건에 대한 식을 입력해야 합니다.  
  
 **Delete**  
 선택한 제약 조건을 테이블에서 제거합니다. CHECK 제약 조건 추가를 취소하려면 이 단추를 사용하여 제약 조건을 제거합니다.  
  
 **일반 범주**  
 확장하면 **식** 속성 필드가 표시됩니다.  
  
 **식**  
 선택한 CHECK 제약 조건의 식을 표시합니다. 새 제약 조건을 만드는 경우 이 상자의 작업을 마치기 전에 식을 입력해야 합니다. 기존 CHECK 제약 조건을 편집할 수도 있습니다. 자세한 내용은 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)을 참조하세요.  
  
 **ID 범주**  
 확장하면 **이름** 및 **설명**에 대한 속성이 표시됩니다.  
  
 **이름**  
 선택한 CHECK 제약 조건의 이름을 표시합니다. 이 제약 조건의 이름을 변경하려면 속성 필드에 직접 텍스트를 입력합니다.  
  
 **설명**  
 CHECK 제약 조건에 대해 설명합니다. 속성 필드에 직접 텍스트를 입력하여 설명을 편집할 수 있고, 속성 필드의 오른쪽에 있는 줄임표( **...** )를 클릭한 다음, **설명 속성** 대화 상자에서 설명을 편집할 수도 있습니다.  
  
 **테이블 디자이너 범주**  
 확장하면 **만들거나 다시 활성화할 때 기존 데이터 검사**, **INSERT 및 UPDATE에 적용**, **복제에 적용**에 대한 속성이 표시됩니다.  
  
 **Check Existing Data On Creation or Re-Enabling**  
 조건 제약에 대해 기존의 모든 데이터 즉, 제약 조건을 만들기 전부터 테이블에 있던 데이터를 검사할지 여부를 지정합니다.  
  
 **INSERT 및 UPDATE에 적용**  
 데이터를 테이블에 삽입하거나 테이블에서 업데이트할 때 제약 조건을 적용할지 여부를 지정합니다.  
  
 **복제에 적용**  
 이 테이블에서 복제 에이전트가 삽입 또는 업데이트를 실행할 때 제약 조건을 적용할지 여부를 나타냅니다.  
  
## <a name="see-also"></a>관련 항목  
 [Unique 제약 조건 및 Check 제약 조건](../../relational-databases/tables/unique-constraints-and-check-constraints.md)   
 [인덱스 및 키 대화 상자 &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
  
