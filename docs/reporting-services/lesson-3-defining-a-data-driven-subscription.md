---
title: '3단원: 데이터 기반 구독 정의 | Microsoft Docs'
ms.custom: ''
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 89197b9b-7502-4fe2-bea3-ed7943eebf3b
caps.latest.revision: 50
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e17d01c4ec9d288a3385c96645a3a8080487a201
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33016876"
---
# <a name="lesson-3-defining-a-data-driven-subscription"></a>Lesson 3: Defining a Data-Driven Subscription
이 [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 자습서 단원에서는 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 웹 포털 데이터 기반 구독 페이지를 사용하여 구독 데이터 원본에 연결하고 구독 데이터를 검색하는 쿼리를 작성하며 결과 집합을 보고서 및 배달 옵션에 매핑합니다.  
  
> [!NOTE]  
> 시작하기 전에 **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에이전트** 서비스가 실행 중인지 확인합니다. 이 서비스를 실행하지 않으면 구독을 저장할 수 없습니다.  한 가지 확인 방법은 [SQL Server 구성 관리자](../relational-databases/sql-server-configuration-manager.md)를 여는 것입니다.
이 단원에서는 1단원 및 2단원을 완료했고 보고서 데이터 원본에서 저장된 자격 증명을 사용한다고 가정합니다.  자세한 내용은 [2단원: 보고서 데이터 원본 속성 수정](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md)을 참조하세요.  
  
## <a name="bkmk_startwizard"></a>데이터 기반 구독 마법사 시작  
  
1.  [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] 웹 포털에서 **홈**을 클릭하고 **Sales Orders** 보고서가 있는 폴더로 이동합니다.  
  
2.  보고서의 상황에 맞는 메뉴 ![ssrs_tutorial_datadriven_reportmenu](../reporting-services/media/ssrs-tutorial-datadriven-reportmenu.png) 에서 **관리**를 클릭한 다음 왼쪽 창에서 **구독** 을 클릭합니다.  
  
3.  **+ 새 구독**을 클릭합니다. 이 단추가 표시되지 않는 경우 내용 관리자 권한이 없는 것입니다. 
  
## <a name="define-a-description"></a>설명 정의  
1.  설명에 **Sales Order 배달** 을 입력합니다.
## <a name="type"></a>설명에
1.  **데이터 기반 구독**을 클릭합니다.  
## <a name="schedule"></a>일정
1. 일정 섹션에서 **보고서별 일정**을 클릭합니다.
2. **일정 편집**을 클릭합니다.
3.  **일정 정보**에서 **한 번**을 누릅니다.  
4.  시작 시간을 현재 시간보다 몇 분 앞당겨 지정합니다.  
5.  **적용**을 클릭합니다.
## <a name="destination"></a>Destination  
1.  대상 섹션에서 배달 방법으로 **Windows 파일 공유** 를 선택합니다.  

## <a name="dataset"></a>Dataset
1. **데이터 집합 편집**을 클릭합니다.
2. **사용자 지정 데이터 원본**을 선택합니다.
3. 데이터 원본 **연결** 유형으로 **Microsoft SQL Server** 를 선택합니다.
4. 연결 문자열에 다음 연결 문자열을 입력합니다. *구독자* 는 1단원에서 만든 데이터베이스입니다. 
  
    ```  
    data source=localhost; initial catalog=Subscribers
    ```
    
 ## <a name="credentials"></a>자격 증명
 1. **다음 자격 증명 사용**을 선택합니다.
 2. **Windows 사용자 이름 및 암호**를 선택합니다.
 3.  **사용자 이름** 및 **암호**에 도메인 사용자 이름 및 암호를 입력합니다. **사용자 이름**을 지정할 때는 도메인 계정과 사용자 계정을 모두 포함합니다.
     > [!NOTE]  
    > 구독자 데이터 원본에 연결하는 데 사용된 자격 증명은 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]로 다시 전달되지 않습니다. 나중에 구독을 수정할 경우 데이터 원본에 연결하는 데 사용된 암호를 다시 입력해야 합니다.
## <a name="query"></a>쿼리      
1.  쿼리 상자에 다음 쿼리를 입력합니다.  
  
    ```  
    Select * from OrderInfo  
    ```  
  
2.  제한 시간을 30초로 지정합니다.  
  
3.  **유효성 검사 쿼리**를 클릭한 다음 **적용**을 클릭합니다.
## <a name="delivery-options"></a>배달 옵션
다음 값을 채웁니다.

매개 변수  |값 원본  | 값/필드  
---------|---------|---------
**파일 이름**     |데이터 집합에서 값 가져오기 | 주문     
**경로**     | 값 입력  | 값에 쓰기 권한이 있는 공용 파일 공유의 이름(예: `\\mycomputer\public\myreports`)을 입력합니다. 
**렌더링 형식** | 데이터 집합에서 값 가져오기 | 형식
**쓰기 모드**| 값 입력| 자동 증분    
**파일 확장명** |값 입력 |True
**사용자 이름** | 값 입력 | 도메인 사용자 계정을 입력합니다. \<domain>\\\<account> 형식으로 입력합니다. 사용자 계정에는 사용자가 구성한 경로에 대한 권한이 있어야 합니다. 
**암호** | 값 입력 | 암호 입력

## <a name="report-parameters"></a>보고서 매개 변수
 1. **OrderNumber** 필드에서 **데이터 집합에서 값 가져오기**를 선택합니다. 값에서 **Order**를 선택합니다. 
 2. **구독 만들기**를 클릭합니다.
   
## <a name="next-steps"></a>Next Steps  
구독을 실행하면 *Subscribers* 데이터 원본의 각 주문에 대해 하나씩 총 4개의 보고서 파일이 사용자가 지정한 파일 공유로 배달됩니다. 각 배달은 데이터(주문별 데이터여야 함), 렌더링 형식 및 파일 형식에 있어 고유해야 합니다. 공유 폴더에서 각 보고서를 열어 각 버전이 사용자가 정의한 구독 옵션을 기반으로 사용자 지정되었는지 확인할 수 있습니다.  
  
![구독으로 만드는 파일 목록](../reporting-services/media/ssrs-tutorial-datadriven-subscription-filelist.gif "구독으로 만드는 파일 목록")  
  
웹 포털의 구독 페이지에는 구독의 **마지막 실행** 날짜와 **상태** 가 표시됩니다. 
**참고:** 업데이트된 정보를 보려면 구독을 실행한 후 페이지를 새로 고칩니다.  
    
![보고서 관리자의 구독 결과](../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png "보고서 관리자의 구독 결과")  
  
이 단계는 "데이터 기반 구독 정의" 자습서의 마지막 단계입니다.   
  
## <a name="see-also"></a>참고 항목  
[구독 및 배달&#40;Reporting Services&#41;](../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
[데이터 기반 구독](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[데이터 기반 구독 만들기, 수정 및 삭제](../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)  
[구독자 데이터에 외부 데이터 원본 사용&#40;데이터 기반 구독&#41;](../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)  
  
  
  

