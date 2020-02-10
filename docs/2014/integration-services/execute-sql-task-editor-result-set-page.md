---
title: SQL 실행 태스크 편집기 (결과 집합 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: d27000c8-8d91-4e1c-b45e-bca9a3c12f6d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d84f7fe551d83f609b2ffc3da92b51eb36b9a595
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058971"
---
# <a name="execute-sql-task-editor-result-set-page"></a>SQL 실행 태스크 편집기(결과 집합 페이지)
  
  **SQL 실행 태스크 편집기** 대화 상자의 **결과 집합** 페이지를 사용하여 SQL 문의 결과를 새 변수 또는 기존 변수로 매핑할 수 있습니다. 일반 페이지의 **ResultSet** 을 **없음**으로 설정한 경우에는 이 대화 상자의 옵션을 사용할 수 없습니다.  
  
 이 태스크에 대한 자세한 내용은 [SQL 실행 태스크](control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 결과 집합](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **결과 이름**  
 
  **추가**를 클릭하여 결과 집합 매핑 집합을 추가한 다음 결과를 설명하는 이름을 제공합니다. 결과 집합 유형에 따라 특정 결과 이름을 사용해야 합니다.  
  
 결과 집합 유형이 **단일 행**이면 쿼리에서 반환한 열 이름이나 쿼리에서 반환한 열의 열 목록에서 열 위치를 나타내는 숫자 중 하나를 사용할 수 있습니다.  
  
 결과 집합 유형이 **전체 결과 집합** 이나 **XML**이면 결과 집합 이름으로 0을 사용해야 합니다.  
  
 **관련 항목**: [SQL 실행 태스크의 결과 집합](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
 **변수 이름**  
 변수를 선택하여 결과 집합을 변수로 매핑하거나 \<**새 변수...**>를 클릭하여 **변수 추가** 대화 상자를 사용하여 새 변수를 추가합니다.  
  
 **추가**  
 결과 집합 매핑을 추가하려면 클릭합니다.  
  
 **제거**  
 목록에서 결과 집합 매핑을 선택한 다음 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 실행 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [SQL 실행 태스크 편집기 &#40;매개 변수 매핑 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)  
  
  
