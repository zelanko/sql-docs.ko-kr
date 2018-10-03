---
title: 데이터 경고 메시지 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 6819720c-d848-4b90-9b51-89501b4f4645
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 5b27eafb4908c74bffaeab7e3f5e8e2ae1bf8f7e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709181"
---
# <a name="data-alert-messages"></a>데이터 경고 메시지

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services 데이터 경고는 데이터 경고 결과가 포함된 메시지와 오류 설명이 포함된 메시지의 두 가지 종류의 데이터 경고 메시지를 전자 메일로 제공합니다. 결과가 포함된 메시지는 모든 받는 사람에게 유용하고 비즈니스 의사 결정을 내리는 데 중요한 보고서 데이터 변경 사항에 대해 알려줍니다. 오류가 발생하여 결과를 사용할 수 없는 경우 오류 메시지를 대신 보냅니다.

또한 데이터 경고 정의 소유자는 데이터 경고 관리자에서 데이터 경고 인스턴스에 대한 정보를 볼 수 있습니다. 자세한 내용은 [Data Alert Manager for SharePoint Users](../reporting-services/data-alert-manager-for-sharepoint-users.md)을 참조하세요.  

> [!NOTE]
> SQL Server 2016 이후부터 SharePoint와의 Reporting Services 통합을 사용할 수 없습니다.
  
##  <a name="DataAlertMessages"></a> 데이터 경고 메시지  
 다음 그림에서는 결과가 포함된 데이터 경고 메시지와 오류 설명이 포함된 경고 메시지를 보여 줍니다.  
  
 **결과 메시지**  
  
 ![결과가 포함된 데이터 경고 전자 메일 메시지](../reporting-services/media/rs-alertmessageresults.gif "결과가 포함된 데이터 경고 전자 메일 메시지")  
  
 **오류 메시지입니다.**  
  
 ![오류 메시지가 포함된 데이터 경고 메시지](../reporting-services/media/rs-alertmessageerrror.gif "오류 메시지가 포함된 데이터 경고 메시지")  
  
 메시지에는 동일한 유형의 정보가 포함되어 있습니다.  
  
1.  **다음 사람 대신** 에는 데이터 경고 정의를 만든 사용자의 이름이 포함되어 있습니다.  
  
2.  경고 정의에 설명을 지정한 경우 설명이 **다음 사람 대신**아래에 표시됩니다.  
  
3.  **경고 결과** 는 경고 정의에 지정된 규칙을 만족하는 보고서 데이터 피드의 행을 테이블 형식으로 표시하거나 오류 설명을 표시합니다. 표시되는 행 수에 대한 제한은 없습니다.  
  
4.  **보고서로 이동** 은 경고 정의가 작성되는 보고서에 대한 링크입니다. 보고서가 이동되거나 삭제되어 링크가 유효하지 않은 경우 오류 메시지가 표시됩니다.  
  
5.  **규칙** 은 경고 정의의 규칙과 절을 나열합니다. 이 정보를 통해 경고 결과를 확인하여 이해하고 결과를 축소하거나 확대하기 위해 변경할 데이터 경고 정의의 규칙을 식별할 수 있습니다.  
  
6.  **보고서 매개 변수** 는 보고서를 실행할 때 사용된 매개 변수와 매개 변수 값을 나열합니다. 매개 변수와 매개 변수 값을 통해 경고 결과를 이해할 수 있습니다.  
  
7.  **컨텍스트 값** 은 보고서 데이터 영역 밖에 있는 보고서 항목의 이름과 값을 나열합니다. 항목은 일반적으로 입력란입니다. 예: 보고서의 제목 또는 설명과 같은 상수 값을 가진 입력란  
  
 두 메시지 형식 간의 유일한 차이점은 항목 5, **경고 결과**입니다. 데이터 경고 인스턴스 또는 데이터 경고 메시지를 만들 때 오류가 발생한 경우 **경고 결과** 에 문제를 설명하는 오류 메시지가 표시됩니다. 모든 받는 사람에게 보낸 오류 메시지를 통해 비즈니스 의사 결정을 내리는 데 필요한 원하는 경고 결과를 사용할 수 없다는 것을 알 수 있습니다.  
  
  
##  <a name="HowTo"></a> 관련 작업  
 이 섹션에는 데이터 경고 메시지에 표시되는 많은 정보를 제공하는 데이터 경고 정의를 만들고 편집하는 방법을 보여 주는 절차가 나열되어 있습니다.  
  
-   [데이터 경고 디자이너에서 데이터 경고 만들기](../reporting-services/create-a-data-alert-in-data-alert-designer.md)  
  
-   [경고 디자이너에서 데이터 경고 편집](../reporting-services/edit-a-data-alert-in-alert-designer.md)  

## <a name="see-also"></a>참고 항목

[데이터 경고 디자이너](../reporting-services/data-alert-designer.md)   
[Reporting Services 데이터 경고](../reporting-services/reporting-services-data-alerts.md)  

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](http://go.microsoft.com/fwlink/?LinkId=620231)
