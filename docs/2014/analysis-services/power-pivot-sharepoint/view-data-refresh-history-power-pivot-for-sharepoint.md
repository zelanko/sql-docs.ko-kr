---
title: 데이터 새로 고침 (SharePoint 용 PowerPivot) 기록 보기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3efe11a733408124490ece2e85c9bd40db34f3fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070915"
---
# <a name="view-data-refresh-history-powerpivot-for-sharepoint"></a>데이터 새로 고침 기록 보기(SharePoint용 PowerPivot)
  데이터 새로 고침 기록은 Excel 통합 문서의 PowerPivot 데이터에 대한 모든 데이터 새로 고침 작업의 레코드입니다. 데이터 새로 고침 작업은 제공된 일정에 따라 SharePoint 팜의 Analysis Services 서버 인스턴스에서 수행됩니다. 기본적으로 데이터 새로 고침 기록은 1년 동안 보존됩니다. 그러나 팜 관리자가 데이터 새로 고침 레코드 보관 기간을 결정하는 사용 및 이벤트 기록에 대한 다른 보존 정책을 지정할 수 있습니다.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **항목 내용**  
  
 [필수 구성 요소](#prereq)  
  
 [개별 통합 문서에 대한 데이터 새로 고침 기록 보기](#viewhistory)  
  
 [모든 통합 문서에 대한 데이터 새로 고침 기록 보기](#viewITOps)  
  
 [기록 정보 사용](#pageelements)  
  
##  <a name="prereq"></a> 사전 요구 사항  
 데이터 새로 고침 기록을 보려면 참가 권한 이상의 권한이 있어야 합니다.  
  
 PowerPivot 데이터가 포함된 통합 문서에서 데이터 새로 고침을 사용하도록 설정하고 예약해야 합니다. 데이터 새로 고침을 예약하지 않은 경우 기록 정보 대신 예약 정의 페이지가 표시됩니다.  
  
##  <a name="viewhistory"></a> 개별 통합 문서에 대한 데이터 새로 고침 기록 보기  
  
1.  SharePoint 사이트에서 PowerPivot 데이터가 포함된 Excel 통합 문서가 있는 라이브러리를 엽니다.  
  
     SharePoint 라이브러리에서 PowerPivot 데이터가 있는 통합 문서를 식별하는 시각적 표시는 없습니다. 새로 고칠 수 있는 PowerPivot 데이터가 포함된 통합 문서를 미리 알고 있어야 합니다.  
  
2.  통합 문서를 선택한 다음 오른쪽에 표시되는 아래쪽 화살표를 클릭합니다.  
  
3.  **PowerPivot 데이터 새로 고침 관리**를 선택합니다.  
  
 현재 Excel 통합 문서의 PowerPivot 데이터에 대한 모든 새로 고침 작업의 전체 레코드를 보여 주는 기록 페이지가 표시됩니다.  
  
##  <a name="viewITOps"></a> 모든 통합 문서에 대한 데이터 새로 고침 기록 보기  
 팜 관리자와 서비스 응용 프로그램 관리자는 중앙 관리의 PowerPivot 관리 대시보드를 사용하여 모든 PowerPivot 통합 문서에 대한 데이터 새로 고침 기록과 상태를 전체적으로 볼 수 있습니다. 자세한 내용은 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)을 참조하세요.  
  
##  <a name="pageelements"></a> 기록 정보 사용  
 데이터 새로 고침 기록 페이지에는 각 새로 고침 작업에 대한 자세한 정보가 제공됩니다. 이 페이지의 정보를 사용하여 새로 고침이 발생했는지 여부와 새로 고침이 실패한 이유를 확인할 수 있습니다.  
  
|항목|Description|  
|----------|-----------------|  
|이름|PowerPivot 데이터가 포함된 Excel 통합 문서의 파일 이름을 지정합니다.|  
|현재 상태|**예약**, **새로 고치는 중**, **성공**또는 **실패**값이 표시됩니다.<br /><br /> **예약** 은 일정을 처음 만들 때 나타납니다. 데이터 새로 고침을 처음 실행한 이후에는 이 상태 메시지가 더 이상 나타나지 않습니다.<br /><br /> **새로 고치는 중** 은 데이터 새로 고침이 진행 중임을 나타냅니다. 요청이 프로세스 큐에 있거나 서버에서 현재 실행되고 있습니다.<br /><br /> **성공** 은 마지막 데이터 새로 고침 작업이 완료되고 업데이트된 통합 문서가 SharePoint 라이브러리에 다시 체크 인되었음을 나타냅니다.<br /><br /> **실패** 는 마지막 데이터 새로 고침 작업이 실패했음을 나타냅니다. 새로 고침 데이터가 저장되지 않았습니다. 통합 문서에 데이터 새로 고침을 시작하기 이전과 동일한 데이터가 포함되어 있습니다.|  
|마지막으로 성공한 새로 고침|마지막 데이터 새로 고침이 성공적으로 완료된 날짜를 지정합니다.|  
|다음에 예정된 새로 고침|다음 데이터 새로 고침이 예약된 날짜를 지정합니다.<br /><br /> **일정 구성** 링크를 누르면 일정 정의 페이지로 이동합니다. 통합 문서에 대한 참가 권한이 있는 경우 링크를 클릭하여 통합 문서의 PowerPivot 데이터에 대한 무인 데이터 새로 고침을 제어하는 일정 정보를 보고 수정할 수 있습니다.|  
|시작됨|기록 세부 정보 섹션에서 **시작됨** 은 실제 처리 시간을 나타냅니다. 실제 처리 시간이 사용자가 예약한 시간과 다를 수 있습니다. 처리는 서버에 사용 가능한 메모리가 충분히 있을 때 시작됩니다. 따라서 서버의 사용량이 많을 경우 지정된 시간보다 몇 시간 뒤에 처리가 시작될 수도 있습니다.|  
|완료|기록 세부 정보 섹션에서 **완료** 는 데이터 새로 고침 작업을 마친 시기를 나타냅니다. 날짜와 시간은 통합 문서가 라이브러리에 다시 체크 인된 시기를 나타냅니다.<br /><br /> 데이터 새로 고침이 실패하면 실패 원인을 설명하는 하나 이상의 메시지가 표시됩니다. 각 레코드를 확장하여 자세한 상태를 확인할 수 있습니다. 각 데이터 원본은 성공 또는 데이터 새로 고침이 완료되지 않은 이유를 설명하는 실패 메시지와 함께 개별적으로 나열됩니다.|  
|Time|데이터 새로 고침이 시작된 시간부터 완료된 시간까지의 누적 시간을 제공합니다.|  
|상태|새로 고침 작업이 성공 또는 실패했는지를 나타내는 기록 레코드를 제공합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [사용 현황 데이터 수집 구성 &#40;SharePoint 용 PowerPivot](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [데이터 새로 고침 예약 &#40;SharePoint 용 PowerPivot&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot 데이터 새로 고침](power-pivot-data-refresh.md)  
  
  
