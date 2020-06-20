---
title: 뷰 이름 바꾸기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5cc76ced033a69788270c3fa9277bcca6972e080
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048912"
---
# <a name="rename-views"></a>뷰 이름 바꾸기
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 뷰 이름을 바꿀 수 있습니다.  
  
> [!WARNING]  
>  뷰의 이름을 바꾸면 해당 뷰와 관련된 코드와 애플리케이션에 문제가 발생할 수 있습니다. 여기에는 기타 뷰, 쿼리, 저장 프로시저, 사용자 정의 함수, 클라이언트 애플리케이션 등이 포함됩니다. 이러한 문제는 연쇄적인 파급 효과를 가져올 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **뷰 이름을 바꾸려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [뷰 이름을 바꾼 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 뷰의 모든 종속성 목록을 가져옵니다. 뷰를 참조하는 모든 개체, 스크립트 또는 애플리케이션은 새 뷰 이름을 반영하도록 수정되어야 합니다. 자세한 내용은 [Get Information About a View](get-information-about-a-view.md)를 참조하세요. 뷰 이름을 바꾸는 것보다 뷰를 삭제하고 새로운 이름으로 다시 만드는 것이 좋습니다. 뷰를 다시 만들면 뷰에 참조된 개체에 대한 종속성 정보가 업데이트됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 SCHEMA에 대한 ALTER 권한, OBJECT에 대한 CONTROL 권한 및 데이터베이스의 CREATE VIEW 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-rename-a-view"></a>뷰 이름을 바꾸려면  
  
1.  **개체 탐색기**에서 이름을 바꿀 뷰가 포함된 데이터베이스를 확장한 다음 **뷰** 폴더를 확장합니다.  
  
2.  이름을 바꿀 뷰를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택합니다.  
  
3.  뷰의 새 이름을 입력합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **뷰 이름을 바꾸려면**  
  
 **sp_rename** 을 사용하여 뷰 이름을 변경할 수도 있지만 기존 뷰를 삭제하고 새 이름으로 뷰를 다시 만드는 것이 좋습니다.  
  
 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql) 및 [DROP VIEW&#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)를 참조하세요.  
  
##  <a name="follow-up-after-renaming-a-view"></a><a name="FollowUp"></a> 후속 작업: 뷰 이름을 바꾼 후  
 뷰의 이전 이름을 참조하는 모든 개체, 스크립트 및 애플리케이션이 이제 새 이름을 사용하는지 확인합니다.  
  
  
