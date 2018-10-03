---
title: 통계 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistics [SQL Server], modifying
- modifying statistics
ms.assetid: b06299ca-ed52-411a-b245-45eac4628c99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0532f2b9ab931eccda5403501a6fe74b3603525c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165843"
---
# <a name="modify-statistics"></a>통계 수정
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 기존 통계를 수정할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계를 수정하려면**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 다음을 만족해야 합니다.  
  
-   사용자에게 테이블이나 뷰에 대한 ALTER 권한이 있어야 합니다.  
  
-   통계를 만들려면 테이블 또는 인덱싱된 뷰의 소유자이거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할 중 하나의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-statistics"></a>통계를 수정하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 통계를 수정할 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 통계를 수정할 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **통계** 폴더를 확장합니다.  
  
5.  수정하려는 통계 개체를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **통계 속성 -** *statistics_name* 대화 상자의 **일반** 페이지에서 **추가**, **제거**, **위로 이동**또는 **아래로 이동**또는 any combination, to alter the properties of the statistics. **통계 열** 표 안에 있는 열의 위치는 통계의 유용성에 큰 영향을 미칠 수 있습니다.  
  
7.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **통계를 수정하려면**  
  
 이 작업은 Transact-SQL 문을 사용하여 수행할 수 없습니다. Transact-SQL을 사용하여 통계를 수정하려면 먼저 기존 통계를 삭제하고 새로운 특성을 사용하여 다시 만들어야 합니다.  
  
 자세한 내용은 [DROP STATISTICS&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-statistics-transact-sql) 및 [CREATE STATISTICS&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql)를 참조하세요.  
  
  
