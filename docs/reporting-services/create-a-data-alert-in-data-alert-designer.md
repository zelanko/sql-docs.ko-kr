---
title: "데이터 경고 디자이너에서 데이터 경고 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8464ab9d-afe1-4490-955f-9f3319bcbf8d
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5203aab062888ca40ee83ee3f00521d6661defba
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-data-alert-in-data-alert-designer"></a>데이터 경고 디자이너에서 데이터 경고 만들기

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../includes/ssrs-appliesto-sql2016-xpreview.md)][!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

데이터 경고 디자이너에서 데이터 경고 정의를 만들 수 있습니다. 경고 정의를 저장한 후 데이터 경고 디자이너에서 해당 정의를 다시 열어 편집한 후 다시 저장할 수 있습니다. 경고 정의 편집에 대한 자세한 내용은 [데이터 경고 관리자에서 내 데이터 경고 관리](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md) 및 [경고 디자이너에서 데이터 경고 편집](../reporting-services/edit-a-data-alert-in-alert-designer.md)을 참조하세요.

> [!NOTE]
> SQL Server 2016 후 SharePoint와 reporting Services 통합을 사용할 수 없습니다.

## <a name="create-a-data-alert-definition"></a>데이터 경고 정의 만들기
 
1.  데이터 경고 정의를 만들 보고서가 포함된 SharePoint 라이브러리를 찾습니다.  
  
2.  보고서를 클릭합니다.  
  
     보고서가 실행됩니다. 보고서에 매개 변수가 있으면 경고 메시지를 받을 대상 데이터가 보고서에 표시되는지 확인합니다. 관심이 있는 열 또는 값이 표시되지 않으면 다른 매개 변수 값을 사용하여 보고서를 다시 실행할 수 있습니다.  
  
    > [!NOTE]  
    >  보고서를 실행하기 위해 선택한 매개 변수 값은 경고 정의에 저장되며 경고 정의 처리 단계의 일환으로 보고서를 다시 실행할 때 사용됩니다. 다른 매개 변수 값을 사용하려면 새 경고 정의를 만들어야 합니다.  
  
3.  **동작** 메뉴에서 **새 데이터 경고**를 클릭합니다.  
  
     다음 그림에서는 **동작** 메뉴를 보여 줍니다.  
  
     ![SharePoint 라이브러리에서 경고 디자이너 열기](../reporting-services/media/rs-openalertdesigneriw.gif "SharePoint 라이브러리에서 경고 디자이너 열기")  
  
     데이터 경고 디자이너가 열리고 보고서가 생성하는 첫 번째 데이터 피드의 처음 100개 행이 테이블에 표시됩니다.  
  
    > [!NOTE]  
    >  **새 데이터 경고** 옵션이 표시되지 않을 경우 경고 서비스가 SharePoint 사이트에 구성되어 있지 않거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 버전에 데이터 경고가 없는 것입니다. 자세한 내용은 [Reporting Services SharePoint Service 및 서비스 응용 프로그램](../reporting-services/report-server-sharepoint/reporting-services-sharepoint-service-and-service-applications.md)을 참조하세요.  
    >   
    >  **새 데이터 경고** 옵션이 회색으로 표시될 경우에는 보고서 데이터 원본이 통합 보안 자격 증명을 사용하거나 자격 증명을 요청하도록 구성되어 있는 것입니다. **새 데이터 경고** 옵션을 사용하려면 저장된 자격 증명을 사용하거나 자격 증명을 아예 사용하지 않도록 데이터 원본을 업데이트해야 합니다.  
  
     데이터 피드의 이름이 **보고서 데이터 이름** 드롭다운 목록에 나타납니다.  
  
4.  필요한 경우 **보고서 데이터 이름** 드롭다운 목록에서 다른 데이터 피드를 선택합니다.  
  
     보고서에서 데이터 피드가 생성되지 않으면 보고서에 대해 경고 정의를 만들 수 없습니다. 보고서의 레이아웃에 따라 각 데이터 피드의 내용이 결정됩니다. 자세한 내용은 [보고서에서 데이터 피드 생성&#40;보고서 작성기 및 SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)을 참조하세요.  
  
5.  필요에 따라 **경고 이름** 텍스트 상자에서 기본 이름을 보다 의미 있는 이름으로 업데이트합니다.  
  
     경고 정의의 기본 이름은 보고서 이름입니다. 경고 정의 이름을 반드시 고유한 이름으로 지정해야 하는 것은 아니지만 이렇게 하지 않으면 나중에 데이터 경고 관리자에서 경고 목록을 볼 때 경고 정의를 구분하기가 어려울 수 있습니다. 따라서 경고 정의에 의미 있고 고유한 이름을 사용하는 것이 좋습니다.  
  
6.  필요에 따라 기본 데이터 옵션을 **데이터 피드의 데이터가 다음을 포함함** 에서 **데이터 피드의 데이터가 다음을 포함하지 않음**으로 변경합니다.  
  
7.  **규칙 추가**를 클릭합니다.  
  
     데이터 피드의 열 목록이 나타납니다.  
  
8.  목록에서 규칙에 사용할 열을 선택한 다음 비교 연산자를 선택하고 임계값을 입력합니다.  
  
     선택한 열의 데이터 형식에 따라 다른 비교 연산자가 나열됩니다. 열에 날짜 데이터 형식이 포함된 경우 해당 규칙의 임계값 옆에 달력 아이콘이 표시됩니다. 달력에서 날짜를 클릭하거나 날짜를 입력하여 데이터를 입력할 수 있습니다.  
  
     데이터 경고 디자이너는 **값 입력 모드** 및 **필드 선택 모드**의 두 가지 비교 모드를 제공합니다. 기본 모드는 **값 입력 모드**입니다. **값 입력 모드** 에 있고 **다음인 경우** 비교를 사용하는 경우에만 OR 절을 추가할 수 있습니다.  
  
9. OR 절을 추가하려면 아래쪽 화살표를 클릭한 다음 **값 입력 모드**를 클릭합니다.  
  
10. 비교 값을 입력합니다.  
  
11. 필요에 따라 줄임표 **(…)** 를 다시 클릭합니다.  
  
     줄임표 **(…)** 는 첫 번째 절을 포함하는 줄에 나타납니다.  
  
     OR 절은 AND 규칙 아래와 해당 규칙 내에 추가됩니다.  
  
12. 필요에 따라 아래쪽 화살표를 클릭하고 **필드 선택 모드**를 선택한 다음 목록에서 열을 선택합니다.  
  
     OR 절을 추가하기 위해 클릭한 줄임표 **(…)** 가 사라집니다.  
  
13. 필요에 따라 **규칙 추가** 를 다시 클릭하여 규칙을 더 추가합니다.  
  
     규칙은 AND 논리 연산자를 사용하여 결합됩니다.  
  
14. 되풀이 목록에서 옵션을 선택합니다. 되풀이 유형에 따라 간격을 입력합니다.  
  
15. 필요에 따라 **고급**을 선택합니다.  
  
16. 필요에 따라 다른 날짜를 입력하거나 달력을 열고 달력에서 날짜를 클릭하여 경고 메시지가 시작될 날짜를 변경합니다.  
  
     기본 시작 날짜는 현재 날짜입니다.  
  
17. 필요에 따라 **경고 중지 시간**옆에 있는 확인란을 선택한 다음 경고 메시지를 중지할 날짜를 선택합니다.  
  
     기본적으로 경고 메시지에는 중지 날짜가 없습니다.  
  
    > [!NOTE]  
    >  경고 메시지를 중지해도 경고 정의는 삭제되지 않습니다. 경고 메시지를 중지한 후 시작 날짜와 중지 날짜를 업데이트하여 해당 메시지를 다시 시작할 수 있습니다. 경고 정의 삭제에 대한 자세한 내용은 [데이터 경고 관리자에서 내 데이터 경고 관리](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md)를 참조하세요.  
  
18. 필요에 따라 **결과가 변경될 때만 메시지 보내기** 확인란의 선택을 취소합니다.  
  
     경고 메시지를 자주 보내는 경우에는 중복된 정보를 방지하기 위해 이 확인란의 선택을 취소하지 마십시오.  
  
19. 경고 메시지를 받는 사람의 전자 메일 주소를 입력합니다. 세미콜론을 사용하여 주소를 구분합니다.  
  
     경고 정의를 만든 사용자의 메일 주소를 사용할 수 있는 경우 **받는 사람** 상자에 추가됩니다.  
  
20. 필요에 따라 **제목** 입력란에서 경고 메시지의 제목 줄을 업데이트합니다.  
  
     기본 제목은 **데이터에 대 한 경고 \<데이터 경고 이름 >**합니다.  
  
21. 필요에 따라 **설명** 입력란에 경고 메시지에 대한 설명을 입력합니다.  
  
22. **저장**을 클릭합니다.  

## <a name="see-also"></a>관련 항목:

[데이터 경고 디자이너](../reporting-services/data-alert-designer.md)   
[경고 담당자를 위한 데이터 경고 관리자입니다.](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services 데이터 경고](../reporting-services/reporting-services-data-alerts.md)  

문의: [Reporting Services 포럼에서 질문](http://go.microsoft.com/fwlink/?LinkId=620231)
