---
title: 보고서에 실행 속성 구성(보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dd821c70f9c3c60451a5e1fe5c73b38a7b64b301
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960079"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>보고서에 실행 속성 구성(보고서 관리자)
  보고서에 대한 데이터를 검색할 시기를 지정하도록 보고서 처리 옵션을 설정할 수 있습니다. 외부 데이터 원본이 특정 시간에 새로 고쳐지고(예: 매일 또는 매주 새로 고쳐지는 데이터 웨어하우스) 보고서가 요청될 때마다 같은 데이터를 검색하는 오버헤드가 발생하지 않도록 하려는 경우에 보고서에 대한 데이터 처리를 예약하는 것이 유용합니다. 외부 데이터베이스 서버의 처리 로드를 제어하거나 동일한 데이터 집합을 사용해야 하는 여러 사용자에게 일관된 결과를 제공하려는 경우에도 데이터 처리를 예약하는 것이 유용합니다. 일시적인 데이터로 요청 시 실행 보고서를 사용하면 매 시간마다 다른 결과를 생성할 수 있습니다. 하지만 보고서 스냅숏을 사용하면 같은 시점의 데이터가 들어 있는 다른 보고서나 분석 도구와 비교하여 유효한 결과를 생성할 수 있습니다.  
  
 보고서 스냅숏은 레이아웃 지침 및 특정 시점에 검색된 쿼리 결과가 들어 있는 보고서입니다. 보고서를 선택할 때 최신 쿼리 결과를 얻을 수 있는 요청 시 실행 보고서와 달리 보고서 스냅숏은 예약된 시간에 처리되고 보고서 서버에 저장됩니다. 표시할 보고서 스냅숏을 선택하면 보고서 서버가 보고서 서버 데이터베이스에서 저장된 보고서를 검색하고 스냅숏이 만들어진 시점에 따른 보고서의 현재 데이터 및 레이아웃을 표시합니다.  
  
 보고서 스냅숏은 특정 렌더링 형식으로 저장되지 않으며 사용자나 애플리케이션이 보고서 스냅숏을 요청할 때만 HTML과 같은 최종 보기 형식으로 렌더링됩니다. 지연된 렌더링은 스냅숏을 이동 가능하게 만듭니다. 요청 디바이스나 웹 브라우저에 적합한 형식으로 보고서를 렌더링할 수 있습니다.  
  
### <a name="to-configure-report-processing-options"></a>보고서 처리 옵션을 구성하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](../report-manager-ssrs-native-mode.md)를 시작합니다.  
  
2.  처리 옵션을 설정할 보고서를 찾아 엽니다.  
  
 보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
1.  드롭다운 메뉴에서 **관리** 를 클릭한 다음 **처리 옵션** 탭을 선택합니다.  
  
2.   **보고서 실행 스냅숏에서 이 보고서 렌더링**을 클릭하고 다음 옵션 중 하나를 선택합니다.  
  
    -   스냅숏을 만들려면 **다음 일정을 사용하여 보고서 실행 스냅숏 만들기**를 선택한 다음 보고서별 일정을 정의하거나 **공유 일정** 목록에서 선택합니다.  
  
    -   스냅숏을 즉시 만들려면 **이 페이지에서 [적용] 단추를 클릭할 때 보고서 스냅숏 만들기**를 선택합니다.  
  
3.  **적용**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 처리 속성 설정](../report-server/set-report-processing-properties.md)   
 [보고서 열기 및 닫기&#40;보고서 관리자&#41;](../reports/open-and-close-a-report-report-manager.md)   
 [내용 페이지&#40;보고서 관리자&#41;](../contents-page-report-manager.md)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [처리 옵션 속성 페이지&#40;보고서 관리자&#41;](../processing-options-properties-page-report-manager.md)  
  
  
