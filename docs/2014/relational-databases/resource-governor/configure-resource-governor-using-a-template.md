---
title: 템플릿을 사용하여 리소스 관리자 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3da27154a824433d214dc495bf7f236ff104274f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198930"
---
# <a name="configure-resource-governor-using-a-template"></a>템플릿을 사용하여 리소스 관리자 구성
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에 제공된 템플릿을 사용하여 리소스 관리자를 구성할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [사용 권한](#Permissions)  
  
-   **작업 그룹을 만들려면**  [템플릿을 사용합니다.](#ConfRGTemplate)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 다음 단계에 따라 리소스 풀과 해당 리소스 풀의 작업 그룹을 만드는 템플릿을 열고 수정할 수 있습니다. 또한 이 템플릿을 사용하여 새 연결을 기본 그룹 또는 만든 작업 그룹으로 라우팅하는 분류자 사용자 정의 함수를 만들 수도 있습니다.  
  
###  <a name="Permissions"></a> Permissions  
 템플릿에서 리소스 관리자 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="ConfRGTemplate"></a> 템플릿을 사용하여 리소스 관리자 구성  
 **다음에서 템플릿을 사용하여 리소스 관리자를 구성하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 클릭합니다.  
  
2.  **템플릿 탐색기**에서 **리소스 관리자**를 확장한 다음 **리소스 관리자 구성**을 두 번 클릭합니다.  
  
3.  **데이터베이스 엔진에 연결**에 필요한 정보를 입력한 다음 **확인**을 클릭합니다. 쿼리 편집기에 Configure Resource Governor.sql 템플릿이 만들어집니다. 이 템플릿을 사용하여 리소스 풀, 작업 그룹 및 분류자 함수를 만들고 구성할 수 있습니다.  
  
4.  템플릿의 값을 변경하려면 Ctrl+Shift+M을 누릅니다. **템플릿 매개 변수 값 지정** 창에 사용할 값을 입력합니다.  
  
5.  템플릿의 변경 내용을 저장하려면 **확인**을 클릭합니다.  
  
6.  쿼리를 실행하려면 **실행**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [리소스 관리자](resource-governor.md)   
 [리소스 관리자 사용](enable-resource-governor.md)   
 [리소스 관리자 리소스 풀](resource-governor-resource-pool.md)   
 [리소스 관리자 작업 그룹](resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](resource-governor-classifier-function.md)   
 [리소스 관리자 속성 보기](view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
