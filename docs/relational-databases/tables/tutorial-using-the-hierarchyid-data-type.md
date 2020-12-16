---
description: '자습서: hierarchyid 데이터 형식 사용'
title: '자습서: hierarchyid 데이터 형식 사용 | Microsoft 문서'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: quickstart
helpviewer_keywords:
- tutorials [hierarchyid]
- hierarchyid [Database Engine], tutorial
ms.assetid: 5a7f7cfd-7faf-439f-8085-8fd6bf7db355
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8aae425506ebc8a2a17aadb2fa9c2d4485fe8f85
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97426745"
---
# <a name="tutorial-using-the-hierarchyid-data-type"></a>자습서: hierarchyid 데이터 형식 사용
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
 이 자습서는 [!INCLUDE[tsql](../../includes/tsql-md.md)]에 대한 경험은 있지만 **hierarchyid** 데이터 형식은 처음 사용하는 사용자를 위해 작성되었습니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
이 자습서는 다음 두 단원으로 이루어져 있습니다.  
  
[1단원: 테이블을 계층 구조로 변환](../../relational-databases/tables/lesson-1-converting-a-table-to-a-hierarchical-structure.md)  
이 단원에서는 부모/자식 계층으로 구조화된 기존 직원 테이블을 가져와 **hierarchyid** 데이터 형식을 사용하여 계층을 나타내는 새 테이블로 데이터를 이동합니다. 이 단원에는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스가 필요합니다.  
  
[2단원: 계층적 테이블의 데이터 만들기 및 관리](../../relational-databases/tables/lesson-2-creating-and-managing-data-in-a-hierarchical-table.md)  
이 단원에서는 **hierarchyid** 데이터 형식을 사용하여 테이블을 만들어 계층 구조를 나타냅니다. 그리고 계층 메서드를 사용하여 테이블의 데이터를 조작하는 방법에 대해 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
시스템에는 다음이 설치되어 있어야 합니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상(버전은 관계 없음)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Express  
  
-   Internet Explorer 6 이상 버전  
  
## <a name="see-also"></a>참고 항목  
[자습서: 데이터베이스 엔진 시작](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
[자습서: Transact-SQL 문 작성](../../t-sql/tutorial-writing-transact-sql-statements.md)  
[hierarchyid 데이터 형식 메서드 참조](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
[계층적 데이터&#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid&#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)  
  
  
