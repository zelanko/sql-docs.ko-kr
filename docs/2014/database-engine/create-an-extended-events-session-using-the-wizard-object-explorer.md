---
title: 마법사 (개체 탐색기)를 사용 하 여 확장된 이벤트 세션 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- Sql12.ssms.XeWizard.Summary.f1
- Sql12.ssms.XeWizard.SetSessionProperties.f1
- Sql12.ssms.XeWizard.CaptureAddFields.f1
- Sql12.ssms.XeWizard.SelectEvents.f1
- Sql12.ssms.XeWizard.SpecifySessionTargets.f1
- Sql12.ssms.XeWizard.Welcome.f1
- sql12.ssms.XeWizard.Welcome.f1
- Sql12.ssms.XeWizard.ChooseTemplate.f1
- Sql12.ssms.XeWizard.SetSessionEventFilters.f1
- Sql12.ssms.XeWizard.Results.f1
helpviewer_keywords:
- Sql11.ssms.XeWizard.CaptureAddFields.f1
- Sql11.ssms.XeWizard.SetSessionEventFilters.f1
- Sql11.ssms.XeWizard.SpecifySessionTargets.f1
- Sql11.ssms.XeWizard.Results.f1
- Sql11.ssms.XeWizard.ChooseTemplate.f1
- Sql11.ssms.XeWizard.SetSessionProperties.f1
- Sql11.ssms.XeWizard.Welcome.f1
- Sql11.ssms.XeWizard.Summary.f1
- Sql11.ssms.XeWizard.SelectEvents.f1
ms.assetid: 80c0456f-17c0-41d8-b2aa-502a2f3bb6de
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc69e3683656c5705e7e82df27b80a8a41cb81a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807365"
---
# <a name="create-an-extended-events-session-using-the-wizard-object-explorer"></a>마법사를 사용하여 확장 이벤트 세션을 만들기(개체 탐색기)
  서버의 이벤트를 손쉽게 선택하고 캡처할 수 있도록 확장 이벤트에는 확장 이벤트 세션을 만드는 단계를 안내해 주는 새 세션 마법사가 포함되어 있습니다. 새 세션 마법사에는 대부분의 확장 이벤트 기능이 표시됩니다. [새 세션 대화 상자](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md) 에서는 데이터를 캡처, 표시 및 분석하는 확장 이벤트 세션을 정의할 수 있습니다. 새 세션 대화 상자에는 모든 확장 이벤트 기능이 표시됩니다.  
  
### <a name="to-open-the-new-session-wizard"></a>새 세션 마법사를 열려면  
  
1.  개체 탐색기에서 **관리** 노드를 확장하고 **확장 이벤트**를 확장합니다.  
  
2.  **세션**을 마우스 오른쪽 단추로 클릭하고 **새 세션 마법사**를 클릭합니다.  
  
### <a name="use-the-following-new-session-wizard-pages-to-create-an-event-session"></a>새 세션 마법사 페이지를 사용하여 이벤트 세션 만들기  
  
-   [소개](#BKMK_Welcome)  
  
-   [세션 속성 설정](#BKMK_SetSessionProperties)  
  
-   [템플릿 선택](#BKMK_ChooseTemplate)  
  
-   [캡처할 이벤트 선택](#BKMK_SelectEventsToCapture)  
  
-   [전역 필드 캡처](#BKMK_CaptureGlobalFields)  
  
-   [세션 이벤트 필터 설정](#BKMK_SetSessionEventFilters)  
  
-   [세션 데이터 저장소 지정](#BKMK_SpecifySessionDataOutput)  
  
-   [요약](#BKMK_Summary)  
  
-   [Create Event Session](#BKMK_CreateEventSession)  
  
##  <a name="BKMK_Welcome"></a> 소개  
 **소개** 페이지에서 다음을 수행합니다.  
  
-   새 세션 마법사의 **소개** 페이지에서 **다음**을 클릭합니다.  
  
     마법사를 두 번 이상 사용하려는 경우 마법사를 시작할 때마다 소개가 나타나지 않도록 하려면 **이 페이지를 다시 표시 안 함** 확인란을 선택합니다.  
  
##  <a name="BKMK_SetSessionProperties"></a> 세션 속성 설정  
 **세션 속성 설정** 페이지에서 다음을 수행합니다.  
  
-   **세션 이름** 상자에 이벤트 세션에 대한 의미 있는 이름을 입력합니다.  
  
     서버를 시작할 때 세션을 시작하려면 **서버 시작 시 이벤트 세션 시작** 확인란을 선택하고 **다음**을 클릭합니다.  
  
##  <a name="BKMK_ChooseTemplate"></a> 템플릿 선택  
 **템플릿 선택** 페이지에서 다음을 수행합니다.  
  
-   일반적인 문제를 위해 디자인된 미리 구성된 템플릿 집합에서 선택하려면 **다음 이벤트 세션 템플릿 사용** 옵션을 선택합니다. 드롭다운 목록에서 사용할 템플릿을 선택하고 **다음**을 클릭합니다.  
  
     -또는-  
  
-   미리 구성된 템플릿을 사용하지 않으려면 **템플릿 사용 안 함** 옵션을 선택하고 **다음**을 클릭합니다.  
  
##  <a name="BKMK_SelectEventsToCapture"></a> 캡처할 이벤트 선택  
 **캡처할 이벤트 선택** 페이지에서 다음을 수행합니다.  
  
1.  **이벤트 라이브러리**에서 캡처할 이벤트를 선택한 다음 오른쪽 화살표를 클릭합니다. 이벤트 라이브러리에서 Shift 키 또는 Ctrl 키를 누른 상태로 각 이벤트를 클릭하여 여러 이벤트를 선택할 수 있습니다.  
  
     드롭다운 목록 상자에서 캡처하려는 이벤트를 검색할 방법을 선택할 수 있습니다. 예를 들어 이벤트 이름을 검색하거나 이벤트 이름과 설명을 검색할 수 있습니다. **이벤트 라이브러리** 상자에 검색할 텍스트를 입력하여 테이블의 단어를 검색할 수 있습니다. 예를 들어 **lock_acquired** 이벤트를 찾으려면 **lock**또는 **lock acquire**를 입력합니다.  
  
     선택한 이벤트는 **선택한 이벤트** 상자에 나타납니다. **선택한 이벤트** 상자에서 이벤트를 제거하려면 왼쪽 화살표를 클릭합니다.  
  
2.  캡처할 이벤트를 선택한 후 **다음**을 클릭합니다.  
  
    > [!NOTE]  
    >  **디버그** 채널의 이벤트는 기본적으로 숨겨져 있습니다. 디버그 이벤트를 표시하려면 **채널** 드롭다운 목록에서 **디버그** 를 선택합니다.  
  
##  <a name="BKMK_CaptureGlobalFields"></a> 전역 필드 캡처  
 동작이라고도 하는 전역 필드를 사용하여 선택한 이벤트에 대한 단일 동작 또는 여러 동작을 연결할 수 있습니다. **템플릿 선택** 페이지에서 템플릿을 선택한 경우 템플릿에 정의된 모든 전역 필드가 이 페이지에 표시됩니다.  
  
 **전역 필드 캡처** 페이지에서 다음을 수행합니다.  
  
-   이벤트 세션에 대해 캡처할 전역 필드를 선택하고 **다음**을 클릭합니다.  
  
     전역 필드 옆의 확인란을 선택하거나 선택 취소하여 전역 필드를 제거 또는 추가할 수 있습니다.  
  
    > [!NOTE]  
    >  선택한 동작은 **이름** 별로 정렬되므로 관련 동작을 사전순으로 볼 수 있습니다. 필드 이름 옆의 열 머리글을 클릭하여 설명이나 사용/사용 안 함 상태별로 정렬할 수도 있습니다.  
  
##  <a name="BKMK_SetSessionEventFilters"></a> 세션 이벤트 필터 설정  
 조건자라고도 하는 필터를 적용하여 캡처할 이벤트를 제한할 수 있습니다. **세션 이벤트 필터 설정** 페이지에서 다음을 수행합니다.  
  
1.  미리 구성된 템플릿을 사용하지 않는 경우 필터 조건을 만들고 **다음**을 클릭합니다.  
  
     미리 구성된 템플릿을 사용하는 경우 새 세션 마법사의 **템플릿의 필터(읽기 전용)** 섹션에 템플릿에서 이미 만들어진 필터가 나열됩니다.  
  
2.  **추가 필터** 섹션에서 이벤트 세션에 대한 추가 필터를 구성할 수 있습니다.  
  
     구성한 필터는 선택한 모든 이벤트에 적용됩니다. 새 세션 마법사에서는 각 이벤트에 대한 필터를 구성할 수 없습니다.  
  
    > [!NOTE]  
    >  필터에 대한 그룹 절을 구성한 경우 결과를 저장하면 중복 괄호가 필터에서 제거됩니다. 예를 들어 필터 그룹 **Clause 1** 및 **Clause 2**를 만든 경우 절 주위에 괄호가 나타납니다. 필터를 저장하면 중복 괄호가 제거됩니다. 괄호가 제거되어도 필터 논리에는 영향이 없습니다.  
  
##  <a name="BKMK_SpecifySessionDataOutput"></a> 세션 데이터 저장소 지정  
 **세션 데이터 저장소 지정** 페이지를 사용하여 분석을 위해 데이터를 수집할 방법을 지정할 수 있습니다. SQL Server 확장 이벤트는 데이터 출력의 대상을 사용합니다. 대상은 이벤트 데이터를 저장하고 파일에 쓰기 및 이벤트 데이터 집계 등의 동작을 수행할 수 있습니다. 분석을 위해 데이터를 수집할 방법을 결정하고 **세션 데이터 스토리지 지정** 페이지에서 다음을 수행합니다.  
  
1.  큰 데이터 집합에 대한 기록 레코드를 만드는 경우 **나중에 분석할 수 있도록 데이터를 파일에 저장합니다.** 확인란을 선택하고 다음을 수행합니다.  
  
    1.  **서버의 파일 이름** 상자에 경로와 파일 이름을 입력하거나, **찾아보기** 를 클릭하여 데이터를 저장할 서버의 파일 디렉터리를 지정합니다.  
  
    2.  **최대 파일 크기** 상자에서 파일 대상에 사용할 최대 파일 크기를 지정합니다. 최대 파일 크기를 지정하지 않으면 디스크가 가득 찰 때까지 파일 크기가 계속 커집니다. 기본 파일 크기는 1GB입니다.  
  
    3.  파일 대상에 대해 파일 롤오버를 사용하도록 설정하려면 **파일 롤오버 사용** 확인란을 선택 합니다.  
  
    4.  **최대 파일 수** 상자에서 파일 시스템에 보관할 최대 파일 수를 지정합니다.  
  
2.  최근 데이터를 수집하려는 경우 **가장 최근 데이터만 사용합니다(ring_buffer 대상)** 확인란을 선택하고 다음을 수행합니다.  
  
    1.  **유지할 이벤트 수** 상자에서 보관할 이벤트 수를 입력하거나 위쪽 및 아래쪽 화살표를 사용하여 선택합니다.  
  
    2.  **최대 버퍼 메모리 크기** 상자에서 사용할 버퍼 메모리의 최대 크기를 지정합니다. 이 값에 도달하면 기존 이벤트가 삭제됩니다.  
  
    3.  버퍼에 각 유형의 특정 이벤트 수를 보관하려면 **버퍼가 꽉 차면 유형당 지정한 개수의 이벤트 유지** 확인란을 선택합니다.  
  
    4.  **유형당 유지할 이벤트 수** 상자에서 보관할 유형당 이벤트 수를 입력하거나 위쪽 및 아래쪽 화살표를 사용하여 선택합니다.  
  
##  <a name="BKMK_Summary"></a> 요약  
 **요약** 페이지에서 다음을 수행합니다.  
  
1.  선택한 내용이 올바른지 확인합니다. 이벤트 세션 노드를 확장하여 선택한 내용이 모두 이벤트 세션에 포함될지 확인합니다.  
  
2.  **스크립트** 를 클릭하여 세션 만들기 스크립트를 새 쿼리 편집기 창으로 내보냅니다.  
  
3.  **마침** 을 클릭하여 이벤트 세션을 만듭니다.  
  
##  <a name="BKMK_CreateEventSession"></a> Create Event Session  
 **이벤트 세션 만들기** 페이지에서 이벤트 세션을 성공적으로 만든 후 다음을 수행합니다.  
  
1.  마법사를 닫은 후 세션을 시작하려면 **세션을 만든 후 즉시 이벤트 세션 시작** 을 클릭합니다. 세션을 만든 후 즉시 이벤트 세션을 시작해야 라이브 데이터를 볼 수 있습니다.  
  
2.  이벤트 세션의 라이브 데이트를 확인하려면 **캡처 시 화면에서 라이브 데이터 감시** 를 클릭합니다. 라이브 데이터는 세션이 만들어진 후 즉시 추적을 표시하기 시작합니다.  
  
## <a name="see-also"></a>관련 항목  
 [새 세션 대화 상자를 사용하여 확장 이벤트 세션 만들기](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md)  
  
  
