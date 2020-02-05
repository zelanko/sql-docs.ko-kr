---
title: Showplan XML Statistics Profile 이벤트를 개별적으로 저장
titleSuffix: SQL Server Profiler
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d15ca528efb0246d1d05c87420045fcc74918886
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74165576"
---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Showplan XML Statistics Profile 이벤트를 개별적으로 저장(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 추적에서 캡처된 **Showplan XML Statistics Profile** 이벤트를 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 개별적인 .SQLPlan 파일로 저장하는 방법에 대해 설명합니다. **에서** Showplan XML Statistics Profile[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 이벤트 파일을 열어 각 이벤트에 대한 그래픽 실행 계획을 볼 수 있습니다.  
  
## <a name="save-showplan-xml-statistics-profile-events-separately"></a>Showplan XML Statistics Profile 이벤트를 개별적으로 저장  
  
1. **파일** 메뉴에서 **새 추적**을 선택한 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
     **추적 속성** 대화 상자가 나타납니다.  
  
    > [!NOTE]  
    >  **연결한 후 즉시 추적 시작**을 선택한 경우에는 **추적 속성** 대화 상자가 나타나지 않고 추적이 시작됩니다. 이 설정을 해제하려면 **도구** 메뉴에서 **옵션**을 선택한 다음 **연결한 후 즉시 추적 시작** 확인란의 선택을 취소합니다.  
  
2. **추적 속성** 대화 상자에서 **추적 이름** 입력란에 추적의 이름을 입력합니다.  
  
3. **템플릿 사용** 목록에서 추적의 기반이 되는 추적 템플릿을 선택합니다. 템플릿을 사용하지 않으려면 **비어 있음**을 선택합니다.  
  
4. 다음 중 하나를 수행합니다.  
  
    -   추적을 파일에 캡처하려면 **파일에 저장** 확인란을 선택합니다. **최대 파일 크기 설정**에 대한 값을 지정합니다.  
  
         또는 **파일 롤오버 사용** 및 **서버에서 추적 데이터 처리** 확인란을 선택합니다. 
  
    -   추적을 데이터베이스 테이블에 캡처하려면 **테이블에 저장** 확인란을 선택합니다.  
  
         필요에 따라 **최대 행 수 설정**을 선택하고 값을 지정합니다.  
  
5. 필요에 따라 **추적 중지 시간 설정** 확인란을 선택하여 중지 날짜 및 시간을 지정합니다. 
  
6. **이벤트 선택** 탭을 선택합니다.  
  
7. **Events** 데이터 열에서 **Performance** 이벤트 범주를 확장한 다음 **Showplan XML Statistics Profile** 확인란을 선택합니다. **Performance** 이벤트 범주가 나타나지 않는 경우 **모든 이벤트 표시**를 선택하여 이 범주를 표시합니다.  
  
     **이벤트 추출 설정** 탭이 **추적 속성** 대화 상자에 추가됩니다.  
  
8. **이벤트 추출 설정** 탭에서 **별도로 XML 실행 계획 이벤트 저장**을 선택합니다.  
  
9. **다른 이름으로 저장** 대화 상자에서 **Showplan XML Statistics Profile** 이벤트를 저장할 파일 이름을 입력합니다.  
  
10. **모든 일괄 처리를 단일 파일로 저장**을 선택하여 **Showplan XML Statistics Profile** 이벤트를 단일 XML 파일로 저장합니다. 또는 **각 XML 실행 계획 일괄 처리를 개별 파일로 저장**을 선택하여 각 **Showplan XML Statistics Profile** 이벤트에 대해 새 XML 파일을 만듭니다.  
  
11. SQL Server Management Studio에서 **Showplan XML Statistics Profile** 이벤트 파일을 보려면 **파일** 메뉴에서 **열기**를 가리킨 다음 **파일**을 선택합니다. **Showplan XML Statistics Profile** 이벤트 파일을 저장한 디렉터리를 찾아본 다음 파일을 선택하여 엽니다. **Showplan XML Statistics Profile** 이벤트 파일의 확장명은 .SQLPlan입니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Profiler에서 Showplan 결과로 쿼리 분석](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
