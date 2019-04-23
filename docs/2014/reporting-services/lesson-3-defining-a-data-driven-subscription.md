---
title: '3단원: 데이터 기반 구독 정의 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eda13c16caf3f123887da00e2c7896d36b8bf7ed
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59945450"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>3단원: 데이터 기반 구독 정의
  이 단원에서는 데이터 기반 구독 페이지를 사용하여 구독 데이터 원본에 연결하고 구독 데이터를 검색하는 쿼리를 작성하며 결과 집합을 보고서 및 배달 옵션에 매핑합니다.  
  
> [!NOTE]  
>  시작하기 전에 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트 서비스가 실행 중인지 확인합니다. 이 서비스를 실행하지 않으면 구독을 저장할 수 없습니다.  
  
 이 단원에서는 1단원 및 2단원을 완료했고 보고서 데이터 원본에서 저장된 자격 증명을 사용한다고 가정합니다.  자세한 내용은 [2단원: 보고서 데이터 원본 속성 수정](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)을 참조하세요.  
  
 항목 내용  
  
-   [데이터 기반 구독 마법사 시작](#bkmk_startwizard)  
  
-   [1 단계-설명 정의](#bkmk_definesubscription)  
  
-   [2 단계-구독자 데이터 원본에 연결을 정의 합니다.](#bkmk_defineconnectiontosubscriber)  
  
-   [3 단계-구독자 데이터를 검색 하는 쿼리 정의](#bkmk_definequery)  
  
-   [4 단계-배달 옵션 설정](#bkmk_set_deliveryoptions)  
  
-   [5 단계-보고서 출력 매개 변수 값을 구성 합니다.](#bkmk_configure_parameter)  
  
-   [6 단계-구독을 예약 하려면](#bkmk_schedule_subscription)  
  
##  <a name="bkmk_startwizard"></a> 데이터 기반 구독 마법사 시작  
  
1.  보고서 관리자에서 **홈**을 클릭하고 **Sales Orders** 보고서가 있는 폴더로 이동합니다.  
  
2.  보고서의 상황에 맞는 메뉴에서 **관리**를 클릭한 후 **구독** 탭을 클릭합니다.  
  
3.  클릭 **새 데이터 기반 구독**합니다. 이 단추가 표시되지 않는 경우 내용 관리자 권한이 없는 것입니다.  
  
##  <a name="bkmk_definesubscription"></a> 1 단계-설명 정의  
  
1.  설명에 **Sales Order 배달** 을 입력합니다.  
  
2.  **받는 사람에게 알림을 보내는 방법 지정** 에서 **Windows 파일 공유**를 선택합니다.  
  
3.  **이 구독에 대해서만 지정하세요**를 선택하고 **다음**을 클릭합니다.  
  
##  <a name="bkmk_defineconnectiontosubscriber"></a> 2 단계-구독자 데이터 원본에 연결을 정의 합니다.  
  
1.  데이터 원본 유형으로 **Microsoft SQL Server** 를 선택합니다.  
  
2.  연결 문자열에 다음 연결 문자열을 입력합니다.  
  
    ```  
    data source=localhost; initial catalog=Subscribers  
    ```  
  
    > [!NOTE]  
    >  구독자는 1단원에서 만든 데이터베이스입니다.  
  
3.  **보고서 서버에 안전하게 저장된 자격 증명**을 클릭합니다.  
  
4.  **사용자 이름** 및 **암호**에 도메인 사용자 이름 및 암호를 입력합니다. **사용자 이름**을 지정할 때는 도메인 계정과 사용자 계정을 모두 포함합니다.  
  
    > [!NOTE]  
    >  구독자 데이터 원본에 연결하는 데 사용된 자격 증명은 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]로 다시 전달되지 않습니다. 나중에 구독을 수정할 경우 데이터 원본에 연결하는 데 사용된 암호를 다시 입력해야 합니다.  
  
5.  **데이터 원본에 연결할 때 Windows 자격 증명으로 사용**을 선택한 후 **다음**을 클릭합니다.  
  
##  <a name="bkmk_definequery"></a> 3 단계-구독자 데이터를 검색 하는 쿼리 정의  
  
1.  쿼리 상자에 다음 쿼리를 입력합니다.  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  제한 시간을 30초로 지정합니다.  
  
3.  **유효성 검사**를 클릭하고 **다음**을 클릭합니다.  
  
##  <a name="bkmk_set_deliveryoptions"></a> 4 단계-배달 옵션 설정  
  
1.  **파일 이름**에 대해 **데이터베이스에서 값 가져오기**를 선택합니다. **Order**필드를 선택합니다.  
  
2.  **경로**에 대해 **정적 값 지정**을 선택합니다. 값 설정에 쓰기 권한이 있는 공용 파일 공유의 이름(예: `\\mycomputer\public\myreports`)을 입력합니다.  
  
3.  **렌더링 형식**에 대해 **데이터베이스에서 값 가져오기**를 선택합니다. **형식**을 선택합니다.  
  
4.  **쓰기 모드**에 대해 **정적 값 지정** 을 선택하고 **AutoIncrement**를 선택합니다.  
  
5.  **파일 확장명**에 대해 **정적 값 지정** 을 선택하고 **True**를 선택합니다.  
  
6.  **사용자 이름**에 대해 **정적 값 지정**을 선택합니다. 도메인 사용자 계정을 입력합니다. 이 계정을 `<domain>\<account>`형식으로 입력합니다. 사용자 계정에는 사용자가 이전 단계에서 구성한 경로에 대한 권한이 있어야 합니다.  
  
7.  **암호**에 대해 **정적 값 지정**을 선택합니다. 암호를 입력합니다. 마법사에서는 암호의 유효성을 검사하지 않으므로 암호 입력 시 주의합니다.  
  
8.  **다음**을 클릭합니다.  
  
##  <a name="bkmk_configure_parameter"></a> 5 단계-보고서 출력 매개 변수 값을 구성 합니다.  
  
1.  **OrderNumber**에 대해 **데이터베이스에서 값 가져오기**를 선택합니다. 값에서 **Order**를 선택합니다. **다음**을 클릭합니다.  
  
##  <a name="bkmk_schedule_subscription"></a> 6 단계-구독을 예약 하려면  
  
1.  **이 구독에 대해 생성된 일정**을 클릭한 후 **다음**을 클릭합니다.  
  
2.  **일정 정보**에서 **한 번**을 누릅니다.  
  
3.  시작 시간을 현재 시간보다 몇 분 앞당겨 지정합니다.  
  
4.  **마침**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
 구독을 실행하면 *Subscribers* 데이터 원본의 각 주문에 대해 하나씩 총 4개의 보고서 파일이 사용자가 지정한 파일 공유로 배달됩니다. 각 배달은 데이터(주문별 데이터여야 함), 렌더링 형식 및 파일 형식에 있어 고유해야 합니다. 공유 폴더에서 각 보고서를 열어 각 버전이 사용자가 정의한 구독 옵션을 기반으로 사용자 지정되었는지 확인할 수 있습니다.  
  
 ![구독으로 만드는 파일 목록](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-filelist.gif "구독으로 만드는 파일 목록")  
  
 보고서 관리자의 구독 페이지에는 구독의 **마지막 실행** 날짜와 **상태** 가 표시됩니다.  
  
> [!NOTE]  
>  업데이트된 정보를 보려면 구독을 실행한 후 페이지를 새로 고칩니다.  
  
 ![보고서 관리자의 구독 결과](../../2014/tutorials/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.gif "보고서 관리자의 구독 결과")  
  
 이 단계는 "데이터 기반 구독 정의" 자습서의 마지막 단계입니다. 다른에 대해 자세히 알아보려면 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 자습서를 참조 하세요 [Reporting Services 자습서 &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 기반 구독 만들기&#40;SSRS 자습서&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [구독 및 배달&#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [만들기, 수정 및 데이터 기반 구독을 삭제 합니다.](subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
