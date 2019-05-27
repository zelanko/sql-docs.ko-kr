---
title: 옵션 (쿼리 결과-SQL Server-결과 그리드 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b67926706674abb116b4f3075089853e6fbb665e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089307"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>옵션 (쿼리 결과-SQL Server-결과 그리드 페이지)
  이 페이지를 사용하여 쿼리 결과 집합을 표 형태로 표시하는 옵션을 지정할 수 있습니다. 이러한 옵션의 변경 사항은 새로운 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리에만 적용됩니다. 현재 쿼리에 대한 옵션을 변경하려면 **쿼리** 메뉴에서 **쿼리 옵션** 을 클릭하거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리 창에서 마우스 오른쪽 단추를 클릭한 다음 **쿼리 옵션**을 선택합니다. **쿼리 옵션** 대화 상자 왼쪽 창의 **결과**에서 **표**를 클릭합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **결과 집합에 쿼리 포함**  
 쿼리 출력의 일부로 쿼리 텍스트를 반환합니다.  
  
 **결과를 복사하거나 저장할 때 열 머리글 포함**  
 결과를 클립보드로 복사하거나 파일로 저장할 때 열 머리글을 포함하려면 이 확인란을 선택합니다. 저장하거나 복사한 결과 데이터에 열 머리글 없이 데이터만 포함시키려면 이 확인란의 선택을 취소합니다.  
  
 **실행 후 결과 삭제**  
 쿼리 결과가 검토 창에 표시되지 않도록 합니다. 실행 후 해당 결과는 곧바로 삭제됩니다. 이 옵션을 지정하면 메모리를 절약할 수 있습니다.  
  
 **별도의 탭에 결과 표시**  
 쿼리 문서 창의 아래쪽 대신 새로운 탭에 결과 집합을 표시하려면 이 확인란을 선택합니다.  
  
 **쿼리 실행 후 결과 탭으로 전환**  
 쿼리 실행 시 화면 포커스를 결과 창으로 자동으로 이동하려면 클릭합니다.  
  
 **검색한 최대 문자 수**  
 **비-XML 데이터**:  
  
 1에서 65535 사이의 숫자를 입력하여 각 셀에 표시될 최대 문자 수를 지정합니다.  
  
> [!NOTE]  
>  너무 많은 문자를 지정하면 결과 집합의 데이터가 잘려 보일 수 있습니다. 각 셀에 표시되는 최대 문자 수는 글꼴 크기에 따라 달라집니다. 이 입력란에 높은 값을 입력하면 큰 결과 집합이 반환될 경우 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 의 메모리 실행 속도가 느려지거나 시스템 성능이 저하될 수 있습니다.  
  
 **XML 데이터**:  
  
 **1MB**, **2MB**또는 **5MB**를 선택합니다. 모든 문자를 검색하려면 **제한 없음** 을 선택합니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
