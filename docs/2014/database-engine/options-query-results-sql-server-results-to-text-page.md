---
title: 옵션 (쿼리 결과-SQL Server-텍스트 페이지로 결과 생성) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToText
ms.assetid: 2ccbdf17-e14f-42f1-a836-ca999a3432c9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f5cdfc761b3b8c19e07b1818c2732414b03258cc
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83856650"
---
# <a name="options-query-results-sql-server-results-to-text-page"></a>옵션 (쿼리 결과-SQL Server-텍스트 페이지로 결과 생성)
  이 페이지를 사용하여 쿼리 결과 집합을 텍스트 형식으로 표시하는 옵션을 지정할 수 있습니다. 이러한 옵션의 변경 내용은 새로운 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 쿼리에만 적용됩니다. 현재 쿼리에 대 한 옵션을 변경 하려면 **쿼리 메뉴에서** **쿼리 옵션** 을 클릭 하거나 쿼리 창에서 마우스 오른쪽 단추 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 를 클릭 한 다음 **쿼리 옵션**을 선택 합니다. **쿼리 옵션** 대화 상자의 **결과**에서 **텍스트**를 클릭합니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 **출력 형식**  
 기본적으로 결과에 공백을 채워 만든 열에 출력됩니다. 이외에 쉼표, 탭 또는 공백을 사용하여 열을 구분하는 옵션이 있습니다. **사용자 지정 구분 기호** 입력란에 다른 구분 문자를 지정하려면 이 드롭다운 목록에서 **사용자 지정 구분 기호** 를 선택합니다.  
  
 **사용자 지정 구분 기호**  
 열을 구분할 문자를 지정합니다. 이 입력란은 **출력 형식** 드롭다운 목록 상자에서 사용자 지정 구분 기호를 클릭한 경우에만 사용할 수 있습니다.  
  
 **결과 집합에 열 머리글 포함**  
 각 열에 열 제목을 붙이지 않으려면 이 확인란의 선택을 취소합니다.  
  
 **결과 집합에 쿼리 포함**  
 결과 창에서 실행되고 있는 쿼리의 텍스트를 쿼리 결과 앞에 표시하려면 이 확인란을 선택합니다.  
  
 **결과를 받는 대로 스크롤**  
 결과 집합 맨 아래의 가장 최근에 반환된 레코드에 포커스를 표시하려면 이 확인란을 선택합니다. 받은 첫 번째 행에 포커스를 표시하려면 이 확인란의 선택을 취소합니다.  
  
 **숫자 값 오른쪽 맞춤**  
 숫자 값을 열 오른쪽에 맞추려면 이 확인란을 선택합니다. 이렇게 하면 고정 소수 자릿수를 가진 숫자를 쉽게 검토할 수 있습니다.  
  
 **쿼리 실행 후 결과 삭제**  
 쿼리 창의 결과 창에 쿼리 결과를 표시한 후 삭제하려면 이 확인란을 선택합니다.  
  
 **별도의 탭에 결과 표시**  
 쿼리 문서 창의 아래쪽 대신 새로운 문서 창에 결과 집합을 표시하려면 이 확인란을 선택합니다.  
  
 **쿼리 실행 후 결과 탭으로 전환**  
 자동으로 화면 포커스를 결과 집합에 두려면 이 확인란을 선택합니다.  
  
 **각 열에 표시할 최대 문자 수**  
 기본값은 256자입니다. 이보다 큰 결과 집합을 잘리지 않게 표시하려면 값을 높입니다. 최대값은 8,192입니다.  
  
 **기본값으로 다시 설정**  
 이 페이지의 모든 값을 원래 기본값으로 다시 설정합니다.  
  
  
