---
title: "튜닝 보고서 보기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-query-tuning
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
helpviewer_keywords: tuning reports [SQL Server]
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
caps.latest.revision: "21"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a3fca4cfcb035c48e37c455e72b03a76474a3cd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-1-3---viewing-tuning-reports"></a>단원 1-3-튜닝 보고서 보기
이 단원의 이전 연습에서 MySession 튜닝 세션의 결과로 생성된 데이터베이스 엔진 튜닝 관리자 구성에서 데이터베이스 개체를 만들거나 삭제하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 보았습니다. MySession 튜닝 세션은 [Tuning a Workload](../../tools/dta/lesson-1-1-tuning-a-workload.md)에서 만들었습니다.  
  
튜닝 결과를 구현하는 데 사용할 수 있는 스크립트를 보면 매우 도움이 되지만 데이터베이스 엔진 튜닝 관리자에서 제공하는 여러 가지 보고서를 보아도 유용합니다. 이러한 보고서는 튜닝하고 있는 데이터베이스의 기존 물리적 디자인 구조와 권장 구조에 대한 정보를 제공합니다. 튜닝 보고서는 다음 연습에서 설명하는 대로 **보고서** 탭을 클릭하여 볼 수 있습니다. 이 연습에서는 [Tuning a Workload](../../tools/dta/lesson-1-1-tuning-a-workload.md) 및 [Viewing Tuning Recommendations](../../tools/dta/lesson-1-2-viewing-tuning-recommendations.md)에서 만든 MySession 및 EvaluateMySession 튜닝 세션을 사용합니다.  
  
### <a name="view-tuning-reports"></a>튜닝 보고서 보기  
  
1.  데이터베이스 엔진 튜닝 관리자를 시작합니다. [데이터베이스 엔진 튜닝 관리자 시작](../../tools/dta/lesson-1-1-launching-database-engine-tuning-advisor.md)을 참조하세요. 이 단원의 이전 연습에서 사용한 것과 같은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결해야 합니다.  
  
    **세션 모니터** 창에서 **MySession** 을 두 번 클릭합니다. 이 세션에서 세션 정보가 로드됩니다.  
  
2.  **보고서** 탭을 클릭합니다.  
  
3.  **튜닝 요약** 창에서 이 튜닝 세션에 대한 정보를 볼 수 있습니다. 스크롤 막대를 사용하여 모든 창 내용을 볼 수 있습니다. **예상 향상률** 과 **권장 구성이 사용하는 공간**을 확인합니다. 튜닝 옵션을 설정할 때 권장 구성이 사용하는 공간을 제한할 수 있습니다. **튜닝 옵션** 탭에서 **고급 옵션**을 선택합니다. **권장 구성에 필요한 최대 공간 정의** 를 선택하고 권장 구성이 사용할 수 있는 최대 공간(MB)을 지정합니다. 도움말 브라우저의 **뒤로** 단추를 사용하여 이 자습서로 돌아올 수 있습니다.  
  
4.  **튜닝 보고서** 창의 **보고서 선택** 목록에서 **문 비용 보고서** 를 클릭합니다. 보고서를 표시할 공간이 더 필요한 경우 **세션 모니터** 창 테두리를 왼쪽으로 끕니다. 데이터베이스의 테이블에 대해 실행되는 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에는 성능 비용이 연결되어 있습니다. 테이블에서 자주 액세스되는 열에 효율적인 인덱스를 만들어 이 성능 비용을 줄일 수 있습니다. 이 보고서에는 작업에서 문을 실행한 경우의 원래 비용과 튜닝 권장 구성이 구현된 경우의 비용 간에 예상되는 향상률이 표시됩니다. 보고서에 포함된 정보의 양은 작업의 길이와 복잡성을 기반으로 합니다.  
  
5.  표 영역에서 **문 비용 보고서** 창을 마우스 오른쪽 단추로 클릭하고 **파일로 내보내기**를 클릭합니다. **MyReport**라는 이름으로 보고서를 저장합니다. 파일 이름에 .xml 확장명이 자동으로 추가됩니다. 즐겨 사용하는 XML 편집기나 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 MyReport.xml을 열어 보고서 내용을 볼 수 있습니다.  
  
6.  데이터베이스 엔진 튜닝 관리자의 **보고서** 탭으로 돌아가서 **문 비용 보고서** 를 마우스 오른쪽 단추로 다시 클릭합니다. 사용 가능한 다른 옵션을 검토합니다. 보고 있는 보고서의 글꼴을 변경할 수 있습니다. 여기에서 글꼴을 변경하면 다른 탭 페이지에서도 변경됩니다.  
  
7.  **보고서 선택** 목록에서 다른 보고서를 클릭하여 보고서에 익숙해집니다.  
  
## <a name="summary"></a>요약  
이제 MySession 튜닝 세션에 대한 데이터베이스 엔진 튜닝 관리자 GUI의 **보고서** 탭을 탐색했습니다. 이와 같은 단계를 사용하여 EvaluateMySession 튜닝 세션에 대해 생성된 보고서를 탐색할 수 있습니다. **세션 모니터** 창에서 **EvaluateMySession** 을 두 번 클릭하여 시작합니다.  
  
## <a name="next-lesson"></a>다음 단원  
[3단원: dta 명령 프롬프트 유틸리티 사용](../../tools/dta/lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
  
