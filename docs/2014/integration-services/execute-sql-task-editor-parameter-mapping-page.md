---
title: SQL 실행 태스크 편집기 (매개 변수 매핑 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.parametermapping.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: 8ebe020a-7921-46b2-8823-398748f379b2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cfbb4468cb69947dfa54fb519b7698286393d578
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437370"
---
# <a name="execute-sql-task-editor-parameter-mapping-page"></a>SQL 실행 태스크 편집기(매개 변수 매핑 페이지)
  **SQL 실행 태스크 편집기** 대화 상자의 **매개 변수 매핑** 페이지를 사용하여 변수를 SQL 문의 매개 변수에 매핑할 수 있습니다.  
  
 이 태스크에 대해 알아보려면 [SQL 실행 태스크](control-flow/execute-sql-task.md) 및 [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **변수 이름**  
 **추가**를 클릭 하 여 매개 변수 매핑을 추가한 후 목록에서 시스템 또는 사용자 정의 변수를 선택 하거나 \<**New variable...**> **변수 추가** 대화 상자를 사용 하 여 새 변수를 추가 하려면 클릭 합니다.  
  
 **관련 항목:** [Integration Services&#40;SSIS&#41; 변수](integration-services-ssis-variables.md)  
  
 **방향**  
 매개 변수의 방향을 선택합니다. 각 변수를 입력 매개 변수, 출력 매개 변수 또는 반환 코드에 매핑합니다.  
  
 **데이터 형식**  
 매개 변수의 데이터 형식을 선택합니다. 사용 가능한 데이터 형식의 목록은 태스크에서 사용하는 연결 관리자에서 선택한 공급자에만 적용됩니다.  
  
 **매개 변수 이름**  
 매개 변수 이름을 입력합니다.  
  
 태스크에서 사용하는 연결 관리자 유형에 따라 숫자 또는 매개 변수 이름을 사용해야 합니다. 일부 연결 관리자 유형의 경우 매개 변수 이름의 첫 문자가 \@ 기호여야 하거나, 이름이 \@Param1과 같은 특정 이름이어야 하거나, 열 이름을 매개 변수 이름으로 지정해야 합니다.  
  
 **관련 항목:** [SQL 실행 태스크의 매개 변수 및 반환 코드](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)  
  
 **매개 변수 크기**  
 문자열 및 이진 필드와 같은 가변 길이를 가지는 매개 변수의 크기를 제공합니다.  
  
 이 설정을 사용하면 공급자에서 가변 길이 매개 변수 값에 대해 충분한 공간을 할당합니다.  
  
 **추가**  
 매개 변수 매핑을 추가하려면 클릭합니다.  
  
 **제거**  
 목록에서 매개 변수 매핑을 선택한 다음 **제거**를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [SQL 실행 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [SQL 실행 태스크 편집기 &#40;결과 집합 페이지&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)   
 [Transact-SQL 참조&#40;데이터베이스 엔진&#41;](/sql/t-sql/language-reference)  
  
  
