---
title: 데이터 경고 관리자에서 내 데이터 경고 관리 | Microsoft Docs
description: 데이터 경고 관리자에서 사용자가 만든 데이터 경고의 목록과 각 경고에 대한 정보를 보는 방법을 알아봅니다.
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: e0e4ffdf-bd4c-4ebd-872b-07486cbb47c2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cd2a6edd53f73eeac5b2033ad399f0a46bee66ab
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245077"
---
# <a name="manage-my-data-alerts-in-data-alert-manager"></a>데이터 경고 관리자에서 내 데이터 경고 관리

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

SharePoint 사용자는 자신이 만든 데이터 경고 목록과 경고에 대한 정보를 볼 수 있습니다. 또한 자신의 경고를 삭제하고, 데이터 경고 디자이너에서 편집할 경고 정의를 열고, 자신의 경고를 실행할 수 있습니다. 다음 그림에서는 데이터 경고 관리자에서 사용자에게 제공되는 기능을 보여 줍니다.

 ![SharePoint 사용자용 경고 관리자 기능](../reporting-services/media/rs-alertmanageriw.gif "SharePoint 사용자용 경고 관리자 기능")

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.

### <a name="to-view-a-list-of-your-alerts"></a>자신의 경고 목록을 보려면  
  
1.  데이터 경고를 만든 보고서를 저장한 SharePoint 라이브러리로 이동합니다.  
  
2.  보고서에서 확장 드롭다운 메뉴 아이콘을 클릭하고 **데이터 경고 관리**를 클릭합니다. 다음 그림에서는 드롭다운 메뉴를 보여 줍니다.  
  
     ![보고서 상황에 맞는 메뉴에서 경고 관리자 열기](../reporting-services/media/rs-openalertmanager.gif "보고서 상황에 맞는 메뉴에서 경고 관리자 열기")  
  
     데이터 경고 관리자가 열립니다. 기본적으로 라이브러리에서 선택된 보고서에 대한 경고가 나열됩니다.  
  
3.  **보고서 경고 보기** 목록 옆에서 아래쪽 화살표를 클릭하고 경고를 볼 보고서를 선택하거나 **모두 표시** 를 클릭하여 모든 경고를 나열합니다.  
  
    > [!NOTE]  
    >  선택한 보고서에 경고가 없으면 경고가 있는 보고서를 찾아 선택하기 위해 SharePoint 라이브러리로 돌아가지 않아도 됩니다. 대신, **모두 표시** 를 클릭하여 모든 경고 목록을 확인합니다.  
  
     테이블에 경고 이름, 보고서 이름, 경고를 만든 자신의 사용자 이름, 경고가 전송된 횟수, 경고 정의가 마지막으로 수정된 시간, 경고 상태가 나열됩니다. 경고를 생성하거나 보낼 수 없으면 상태 열에 오류에 대한 정보가 포함되어 문제를 해결하도록 돕습니다.  
  
### <a name="to-edit-an-alert-definition"></a>경고 정의를 편집하려면  
  
-   경고 정의를 편집할 데이터 경고를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭합니다.  
  
     경고 정의가 데이터 경고 디자이너에서 열립니다. 자세한 내용은 [경고 디자이너에서 데이터 경고 편집](../reporting-services/edit-a-data-alert-in-alert-designer.md) 및 [데이터 경고 디자이너](../reporting-services/data-alert-designer.md)를 참조하세요.  
  
    > [!NOTE]  
    >  데이터 경고 정의를 만든 사용자만 해당 정의를 편집할 수 있습니다.  
  
    > [!NOTE]  
    >  보고서가 변경되고 보고서에서 생성된 데이터 피드가 변경된 경우 경고 정의가 더 이상 유효하지 않을 수 있습니다. 이러한 예로는 해당 규칙에서 경고가 참조하는 열이 보고서에서 삭제되었거나, 데이터 형식을 변경하거나, 다른 데이터 피드에 포함되는 경우 또는 보고서가 삭제 또는 이동되는 경우를 들 수 있습니다. 유효하지 않은 경고 정의를 열 수는 있지만 정의를 작성할 때 사용한 보고서 데이터 피드의 현재 버전을 기준으로 유효한 경고 정의만 다시 저장할 수 있습니다. 보고서에서 데이터 피드를 생성하는 방법은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
### <a name="to-delete-an-alert-definition"></a>경고 정의를 삭제하려면  
  
-   삭제할 데이터 경고를 마우스 오른쪽 단추로 클릭하고 **삭제**를 클릭합니다.  
  
     경고를 삭제하면 더 이상 경고 메시지가 전송되지 않습니다.  
  
### <a name="to-run-an-alert"></a>경고를 실행하려면  
  
-   실행할 데이터 경고를 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.  
  
     데이터 경고 디자이너에서 지정한 일정 옵션에 관계없이 경고 인스턴스가 생성되고 데이터 경고 메시지가 즉시 전송됩니다. 예를 들어 매주, 그리고 결과가 변경된 경우에만 전송되도록 구성된 경고가 전송됩니다.  

## <a name="see-also"></a>참고 항목

[경고 담당자를 위한 데이터 경고 관리자](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services 데이터 경고](../reporting-services/reporting-services-data-alerts.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
