---
title: 보고서 실행 속성 구성 - Reporting Services | Microsoft Docs
description: 보고서가 요청될 때마다 동일한 데이터를 검색하는 오버헤드를 방지하기 위해 보고서 처리 옵션을 설정하여 보고서 데이터 검색 시기를 지정하는 방법을 알아봅니다.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5f30c3e123c80b9a16fd020e3126a3c40f366834
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510174"
---
# <a name="configure-execution-properties-for-a-report"></a>보고서 실행 속성 구성
  보고서에 대한 데이터를 검색할 시기를 지정하도록 보고서 처리 옵션을 설정할 수 있습니다. 외부 데이터 원본이 특정 시간에 새로 고쳐지고(예: 매일 또는 매주 새로 고쳐지는 데이터 웨어하우스) 보고서가 요청될 때마다 같은 데이터를 검색하는 오버헤드가 발생하지 않도록 하려는 경우에 보고서에 대한 데이터 처리를 예약하는 것이 유용합니다. 외부 데이터베이스 서버의 처리 로드를 제어하거나 동일한 데이터 집합을 사용해야 하는 여러 사용자에게 일관된 결과를 제공하려는 경우에도 데이터 처리를 예약하는 것이 유용합니다. 일시적인 데이터로 요청 시 실행 보고서를 사용하면 매 시간마다 다른 결과를 생성할 수 있습니다. 하지만 보고서 스냅샷을 사용하면 같은 시점의 데이터가 들어 있는 다른 보고서나 분석 도구와 비교하여 유효한 결과를 생성할 수 있습니다.  
  
 보고서 스냅샷은 레이아웃 지침 및 특정 시점에 검색된 쿼리 결과가 들어 있는 보고서입니다. 보고서를 선택할 때 최신 쿼리 결과를 얻을 수 있는 요청 시 실행 보고서와 달리 보고서 스냅샷은 예약된 시간에 처리되고 보고서 서버에 저장됩니다. 표시할 보고서 스냅샷을 선택하면 보고서 서버가 보고서 서버 데이터베이스에서 저장된 보고서를 검색하고 스냅샷이 만들어진 시점에 따른 보고서의 현재 데이터 및 레이아웃을 표시합니다.  
  
 보고서 스냅샷은 특정 렌더링 형식으로 저장되지 않으며 사용자나 애플리케이션이 보고서 스냅샷을 요청할 때만 HTML과 같은 최종 보기 형식으로 렌더링됩니다. 지연된 렌더링은 스냅샷을 이동 가능하게 만듭니다. 요청 디바이스나 웹 브라우저에 적합한 형식으로 보고서를 렌더링할 수 있습니다.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-processing-options"></a>보고서 처리 옵션을 구성하려면  
  
1.  [보고서 관리자&#40;SSRS 기본 모드&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)를 시작합니다.  
  
2.  처리 옵션을 설정할 보고서를 찾아 엽니다.  
  
 보고서 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
1.  드롭다운 메뉴에서 **관리** 를 클릭한 다음 **처리 옵션** 탭을 선택합니다.  
  
2.  **보고서 실행 스냅샷에서 이 보고서 렌더링**을 클릭하고 다음 옵션 중 하나를 선택합니다.  
  
    -   스냅샷을 만들려면 **다음 일정을 사용하여 보고서 실행 스냅샷 만들기**를 선택한 다음 보고서별 일정을 정의하거나 **공유 일정** 목록에서 선택합니다.  
  
    -   스냅샷을 즉시 만들려면 **이 페이지에서 [적용] 단추를 클릭할 때 보고서 스냅샷 만들기**를 선택합니다.  
  
3.  **적용**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [내용 페이지&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [보고서 서버 콘텐츠 관리&#40;SSRS 기본 모드&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [처리 옵션 속성 페이지&#40;보고서 관리자&#41;](https://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)  
  
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="to-configure-report-execution-properties"></a>보고서 실행 속성을 구성하려면  
  
[보고서 서버의 웹 포털(SSRS 기본 모드)](../../reporting-services/web-portal-ssrs-native-mode.md)에서 다음을 수행합니다.  
  
1. 실행 속성을 구성하려는 보고서로 이동합니다.  
  
2. 보고서를 마우스 오른쪽 단추로 클릭하고 드롭다운 메뉴에서 **관리**를 선택합니다.

3. **기록 스냅샷** 탭을 선택하여 **기록 스냅샷** 페이지를 표시합니다.  
  
4. **일정 및 설정** 단추를 선택하고 아직 확인 표시하지 않았다면 **일정에 따라 기록 스냅샷 만들기**를 확인 표시합니다.
  
5. 원하는 대로 **공유 일정** 또는 **보고서별 일정**을 선택합니다.  
  
6. **고급** 섹션의 기록 스냅샷에서 원하는 **보존** 정책을 선택합니다.  
  
7. **적용**을 선택합니다.  
  
   >[!NOTE]
   >즉시 스냅샷을 만들려면 **일정 및 설정** 단추 대신에 **새 기록 스냅샷**을 선택합니다. 그러면 보고서 스냅샷이 즉시 생성됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   
 [보고서 서버 콘텐츠 관리(SSRS 기본 모드)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [보고서 처리 속성 설정](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end