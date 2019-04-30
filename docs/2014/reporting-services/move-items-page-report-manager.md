---
title: 이동 항목 페이지 (보고서 관리자) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: acee0f51707a0535f0d6f63152cdf461ad50f46c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188443"
---
# <a name="move-items-page-report-manager"></a>항목 이동 페이지(보고서 관리자)
  항목 이동 페이지를 사용하여 보고서, 폴더 또는 기타 항목을 보고서 서버의 새 위치로 이동할 수 있습니다. 새 위치의 경로를 입력하거나 트리 뷰를 사용하여 보고서 서버 네임스페이스에서 새 위치를 찾아볼 수 있습니다. 현재 보고서 서버에 저장되어 있고 이동 권한 있는 항목만 이동할 수 있습니다.  
  
 다른 항목에서 참조하는 항목(예: 많은 보고서가 참조하는 공유 데이터 원본 또는 모델)을 이동할 때는 해당 항목에 대한 경로 정보가 자동으로 업데이트됩니다. 공유 데이터 원본을 이동해도 이를 사용하는 보고서 및 모델에 대한 데이터 원본 연결은 끊어지지 않습니다. 사용자에게 사용 권한이 없는 폴더로 공유 데이터 원본 또는 모델을 이동하는 경우 사용자는 이를 참조하는 보고서를 계속 실행할 수 있지만 폴더 계층 구조에서 이러한 항목을 볼 수는 없습니다.  
  
 **위치**에 루트 폴더 이름으로 시작하는 전체 폴더 경로를 지정합니다. 경로 이름을 입력하거나 트리 뷰를 사용하여 원하는 폴더로 이동할 수 있습니다.  
  
> [!NOTE]  
>  모든 항목을 이동할 수 있는 것은 아닙니다. 홈, 내 보고서, 사용자 폴더와 같이 예약된 폴더는 이동할 수 없습니다. 보고서 기록이나 스냅숏은 다른 위치로 이동할 수 없습니다. 기록 및 스냅숏은 항상 기반이 되는 보고서와 함께 저장되며 이 보고서를 통해 액세스됩니다.  
  
## <a name="navigation"></a>탐색  
 사용자 인터페이스(UI)에서 이 위치를 탐색하려면 다음 절차를 사용하십시오.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>자세히 보기의 내용 페이지에서 항목 이동 페이지를 열려면  
  
1.  보고서 관리자를 열고 이동할 항목이 있는 폴더로 이동합니다. 보고서 관리자 홈 페이지에서 항목을 이동할 수도 있습니다.  
  
2.  도구 모음에서 **자세히 보기**를 클릭합니다.  
  
    > [!NOTE]  
    >  **바둑판식 배열 보기**만 표시된다면 이미 **자세히 보기**상태인 것입니다.  
  
3.  항목 옆의 확인란을 선택한 다음 도구 모음에서 **이동** 을 클릭합니다. 항목 여러 개를 동일한 새 위치로 이동하려는 경우 확인란 여러 개를 선택할 수 있습니다.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>바둑판식 배열 보기의 내용 페이지에서 항목 이동 페이지를 열려면  
  
1.  보고서 관리자를 열고 이동할 항목이 있는 폴더로 이동합니다. 보고서 관리자 홈 페이지에서 항목을 이동할 수도 있습니다.  
  
2.  도구 모음에서 **바둑판식 배열 보기**를 클릭합니다.  
  
    > [!NOTE]  
    >  **자세히 보기**만 표시된다면 이미 **바둑판식 배열 보기**상태인 것입니다.  
  
3.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
4.  드롭다운 메뉴에서 **이동**을 클릭합니다.  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>항목의 일반 속성 페이지에서 항목 이동 페이지를 열려면  
  
1.  보고서 관리자를 열고 이동할 항목이 있는 폴더로 이동합니다. 보고서 관리자 홈 페이지에서 항목을 이동할 수도 있습니다.  
  
2.  항목 위로 마우스를 이동하여 드롭다운 화살표를 클릭합니다.  
  
3.  드롭다운 메뉴에서 **관리**를 클릭합니다. 항목의 일반 속성 페이지가 열립니다.  
  
4.  항목 도구 모음에서 **이동**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [일반 속성 페이지, 폴더 &#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [일반 속성 페이지, 보고서&#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [일반 속성 페이지, 리소스 &#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [일반 속성 페이지, 공유 데이터 원본 &#40;보고서 관리자&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [보고서 관리자 F1 도움말](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
