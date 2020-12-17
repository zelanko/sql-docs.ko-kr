---
title: 보고서 기록 제한 - Reporting Services | Microsoft Docs
description: 보고서 서버의 보고서 기록을 구성하는 방법을 알아봅니다. 특정 보고서의 보고서 기록을 구성하는 방법도 알아봅니다.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d01a008e00d2effccb109555799bbe6d55baf1e3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466574"
---
# <a name="limit-report-history---reporting-services"></a>보고서 기록 제한 - Reporting Services
  보고서 기록은 시간에 따라 만든 보고서 스냅샷의 모음입니다. 요청 시 보고서 기록을 만들거나 스냅샷이 만들어져 보고서 기록에 추가되는 빈도를 예약할 수 있습니다.  
  
 보고서 기록은 보고서 서버 데이터베이스에 저장됩니다. 보고서 스냅샷에 많은 양의 데이터가 포함된 경우 데이터베이스 크기에 영향을 주는 스냅샷 보존이 최소화되도록 보고서 기록을 제한해야 합니다.  

::: moniker range="=sql-server-2016"
  
## <a name="to-configure-report-history-for-a-report-server"></a>보고서 서버에 대한 보고서 기록을 구성하려면  
  
1.  보고서 관리자의 일반 도구 모음에서 **사이트 설정** 을 클릭합니다.  
  
2.  모든 보고서 기록을 무제한 보관하려면 **보고서 기록에 스냅샷을 무제한으로 보관** 을 선택합니다. 그렇지 않은 경우 **보고서 기록의 복사본 개수 제한** 을 선택하여 지정된 보고서에 대해 보관할 수 있는 스냅샷의 최대 수를 지정합니다.  
  
3.  **적용** 을 클릭합니다.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>특정 보고서에 대한 보고서 기록을 구성하려면  
  
1.  보고서 관리자에서 기록을 구성하려는 보고서로 이동한 후 보고서를 클릭하여 엽니다.  
  
2.  **속성** 탭을 클릭합니다.  
  
3.  **기록** 탭을 클릭합니다.  
  
4.  보고서에 대한 옵션을 선택하고 **적용** 을 클릭합니다. 각 옵션에 대한 자세한 내용은 [스냅샷 옵션 속성 페이지&#40;보고서 관리자&#41;](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 기록에 스냅샷 추가&#40;보고서 관리자&#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [보고서 관리자&#40;SSRS 기본 모드&#41;](../web-portal-ssrs-native-mode.md)  

::: moniker-end

::: moniker range=">=sql-server-2017"

## <a name="to-configure-report-history-for-a-report-server"></a>보고서 서버에 대한 보고서 기록을 구성하려면  
  
1.  웹 포털의 글로벌 도구 모음에서 **사이트 설정** 을 클릭합니다.  
  
2.  모든 보고서 기록을 무제한 보관하려면 **보고서 기록에 스냅샷을 무제한으로 보관** 을 선택합니다. 그렇지 않은 경우 **보고서 기록의 복사본 개수 제한** 을 선택하여 지정된 보고서에 대해 보관할 수 있는 스냅샷의 최대 수를 지정합니다.  
  
3.  **적용** 을 클릭합니다.  
  
## <a name="to-configure-report-history-for-a-specific-report"></a>특정 보고서에 대한 보고서 기록을 구성하려면  
  
1.  웹 포털에서 기록을 구성하려는 보고서로 이동한 다음, 보고서를 클릭하여 엽니다.  
  
2.  **속성** 탭을 클릭합니다.  
  
3.  **기록** 탭을 클릭합니다.  
  
4.  보고서에 대한 옵션을 선택하고 **적용** 을 클릭합니다. 각 옵션에 대한 자세한 내용은 [스냅샷 옵션 속성 페이지](/previous-versions/sql/sql-server-2016/ms189952(v=sql.130))를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [보고서 기록에 스냅샷 추가](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   

::: moniker-end
