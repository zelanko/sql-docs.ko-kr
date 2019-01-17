---
title: 'SQL Server 모바일 보고서: 종단 간 연습'
description: Reporting Services 웹 포털의 SQL Server 모바일 보고서 게시자를 사용하여 모든 화면 크기에 적합한 모바일 보고서를 만들고 Power BI 모바일 앱에 표시하는 방법을 알아봅니다.
ms.date: 12/07/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: e198575e-b154-4342-b944-2bf19ec49bfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: db6f8c664dff6f7234e43a3e3f11f6cc01e2eac4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209712"
---
# <a name="sql-server-mobile-reports-end-to-end-walk-through"></a>SQL Server 모바일 보고서: 종단 간 연습
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] 웹 포털의 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 를 사용하여 모든 화면 크기에 적합한 모바일 보고서를 만들고 Power BI 모바일 앱에 표시하는 방법을 알아봅니다.

조정 가능한 표 행/열이 표시된 디자인 화면에서 유동적인 모바일 보고서 요소를 사용하여 모바일 보고서를 만듭니다. 다양한 온-프레미스 데이터 원본에 연결하거나 Excel 통합 문서를 업로드하여 모바일 보고서를 만듭니다. 그런 다음 보고서를 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에 저장하고 브라우저 또는 Power BI 모바일 앱에서 확인합니다.  
  
이 문서에서는 다음 작업을 안내합니다.   
  
- AdventureWorks 데이터베이스를 예제 데이터 원본으로 사용하여 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에서 공유 데이터 원본 및 데이터 세트 만들기.  
- [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]에서 Reporting Services 모바일 보고서 만들기  
- [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에 모바일 보고서 게시  
- Power BI 모바일 앱에서 모바일 보고서 보기  
  
## <a name="before-we-start"></a>시작하기 전에  
이러한 단계를 따르려면 다음 제품이 필요합니다.  
  
* 데이터 원본 및 KPI를 만들고 데이터 세트 및 모바일 보고서를 게시하려면 [Reporting Services 기본 모드 보고서 서버](../install-windows/install-reporting-services-native-mode-report-server.md)에 액세스해야 합니다.  
* 공유 데이터 세트를 만들려면 [보고서 작성기를 설치](../install-windows/install-report-builder.md)합니다.  
* 모바일 보고서를 만들려면 [SQL Server 모바일 보고서 게시자를 설치](https://go.microsoft.com/fwlink/?LinkId=717766)합니다.  
* [AdventureWorks 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)  
*  또는 [Microsoft SQL Server 샘플](../../sample/microsoft-sql-server-samples.md) 페이지에서 제공되는 Wide World Importers 샘플 데이터베이스.
* 결과를 보려면 
  *   [Power BI 서비스에 등록](https://go.microsoft.com/fwlink/?LinkID=513879) 합니다.
  *  모바일 디바이스(iOS, Android 휴대폰 또는 Windows 10 디바이스)에[Power BI 모바일 앱을 다운로드](https://docs.microsoft.com/en-us/power-bi/consumer/mobile/mobile-apps-for-mobile-devices) 합니다.  

  
## <a name="create-a-shared-data-source"></a>공유 데이터 원본 만들기  
  
Reporting Services에서 지원하는 모든 데이터 원본에서 모바일 보고서에 대한 공유 데이터 원본을 만들 수 있습니다. [지원되는 데이터 원본 목록](../report-data/data-sources-supported-by-reporting-services-ssrs.md)을 참조하세요.  
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에서 **새로 만들기** > **데이터 원본**을 클릭합니다.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
3. 데이터 원본 정보를 입력하고 **확인**을 클릭합니다.  
  
    기본적으로 데이터 원본은 포털에 표시되지 않습니다.    
   
5. 데이터 원본을 보려면 **표시** > **데이터 원본**을 클릭합니다.  
  
   ![PBI_SSMRP_DisplayDataSources](../../reporting-services/mobile-reports/media/pbi-ssmrp-displaydatasources.png)  
   
6. 이제 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 포털에 데이터 원본이 표시됩니다.  
  
   ![PBI_SSMRP_PortlDataSource](../../reporting-services/mobile-reports/media/pbi-ssmrp-portldatasource.png)  
  
[Reporting Services의 공유 데이터 원본](../report-data/create-modify-and-delete-shared-data-sources-ssrs.md)에 대해 자세히 알아보세요.  
   
## <a name="shared-dataset">공유 데이터 세트 만들기</a>  
  
기존 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 클라이언트 도구(예: [!INCLUDE[ssBIDevStudioFull_md](../../includes/ssbidevstudiofull-md.md)]의 보고서 디자이너)를 사용하여 공유 데이터 세트를 만듭니다.  이 연습에서는 [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]를 사용합니다. [보고서 작성기를 설치](../install-windows/install-report-builder.md)하거나 웹 포털에서 시작합니다. 세 개의 데이터 세트, 즉 KPI 값에 대한 데이터 세트, KPI 추세에 데이터 세트 및 Reporting Services 모바일 보고서의 추가 필드가 포함된 데이터 세트를 만듭니다.     
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에서 **새로 만들기** > **페이지가 매겨진 보고서** 를 클릭하여 [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]를 시작합니다.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)   
2. **새 데이터 세트**를 클릭합니다.  
  
   ![PBI_SSMRP_RBNewDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-rbnewdataset.png)  
   
3. **다른 데이터 원본 찾아보기**를 클릭합니다.  
   
4. 이름 필드에 데이터 원본을 저장한 서버의 이름을 다음 형식으로 입력합니다.   
   
   이름: https://*localhost*/ReportServer  
   항목 유형: 데이터 원본(*.rsds)  
   
5. **열기**를 클릭하여 해당 서버에서 만든 데이터 원본으로 이동합니다.  
   
6. 데이터 원본을 선택하고 **열기** 를 다시 클릭합니다.    
  
7. [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]에서 데이터 세트를 디자인합니다.  
  
   ![PBI_SSMRP_RB_QueryDesignr600](../../reporting-services/mobile-reports/media/pbi-ssmrp-rb-querydesignr600.png)  
   
8. 완료되면 데이터 세트를 [!INCLUDE[PRODUCT_NAME](../../includes/ssrs.md)] 보고서 서버에 저장합니다.    
   
이제 이 데이터 세트를 KPI 및 모바일 보고서의 기초로 사용할 수 있습니다.  동일한 데이터 원본에 대해 여러 데이터 세트를 만들 수 있습니다. 또한 이러한 공유 데이터 세트에 대해 여러 KPI 및 모바일 보고서를 만들 수 있습니다.   
  
## <a name="create-KPI">KPI 만들기</a>  
[!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에서 바로 KPI를 만듭니다.    
  
1. 웹 포털 오른쪽 위에서 **새로 만들기** > **새 KPI**를 클릭합니다.   
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
      
   KPI 만들기 화면에서 수동으로 값을 입력하거나 공유 데이터 세트를 사용할 수 있습니다.    
2. **값**을 **수동 설정**에서 **데이터 세트 필드**로 변경합니다.  
   
   ![PBI_SSMRP_KPI_DatasetField](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpi-datasetfield.png)  
   
3. **데이터 세트 필드 선택**상자에서 줄임표( **...** )를 클릭하고 이전 단계에서 데이터 세트를 선택합니다.  
   
   ![PBI_SSMRP_KPIPickDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickdataset.png)  
   
4. 데이터 세트에서 필드를 선택합니다.    
   
   ![PBI_SSMRP_KPIPickDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickfield.png)  
     
5. 원하는 집계를 선택합니다. KPI는 숫자만 표시할 수 있으므로 이 숫자를 표시하도록 필드가 집계됩니다.

   ![reporting-services-kpi-pick-aggregation](../../reporting-services/mobile-reports/media/reporting-services-kpi-pick-aggregation.png)

6. **확인**을 클릭합니다.

7. **추세 집합** 상자에서 **데이터 세트 추세**를 클릭합니다.  
  
6. **데이터 세트 추세 선택** 상자에서 줄임표(**...**)를 클릭합니다.  
   
7. 필드를 선택하고 **확인**을 클릭합니다.  

   ![PBI_SSMRP_KPIPickTrend](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipicktrend.png)  
  
8. KPI의 이름을 지정하고 시각화 유형을 선택한 후 **만들기**를 클릭합니다.   
  
   KPI가 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에 표시됩니다.  
   
    ![PBI_SSMRP_NewKPI](../../reporting-services/mobile-reports/media/pbi-ssmrp-newkpi.png)  
    
## <a name="create-mobile-report">Reporting Services 모바일 보고서 만들기</a>  
   
Reporting Services 모바일 보고서를 만들려면 [SQL Server Mobile 보고서 게시자를 설치](https://go.microsoft.com/fwlink/?LinkId=717766)하거나 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 웹 포털에서 시작합니다. 

[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]를 처음 열면 모바일 보고서를 만들 수 있는 빈 캔버스가 표시됩니다. 먼저 시각적 개체를 만들거나 데이터로 시작할 수 있습니다. 시각적 개체를 먼저 만든 경우 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 는 보고서에 연결된 시뮬레이션 데이터를 자동으로 생성하고 사용자가 시각적 선택 항목을 변경할 때 이를 동적으로 변경합니다. 직접 연습해 보세요.   
  
## <a name="start-with-the-visuals"></a>시각적 개체로 시작  
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에서 **새로 만들기** > **모바일 보고서** 를 클릭하여 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]를 시작합니다.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)

   [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 가 마스터 레이아웃 눈금으로 열립니다.  
  
2. **레이아웃** 탭에서 차트 섹션까지 아래로 스크롤합니다.  
  
   ![PBI_SSMRP_LayoutTabCharts2](../../reporting-services/mobile-reports/media/pbi-ssmrp-layouttabcharts2.png)  
  
2. **트리 맵** 을 눈금으로 끈 다음 오른쪽 아래 모서리를 끌어 세 개의 열과 세 개의 행으로 만듭니다.  
  
   ![PBI_SSMRP_TreeMap](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemap.png)  
  
3. 맨 아래에서 해당 시각적 속성을 볼 수 있습니다. 모두 보려면 옆쪽으로 스크롤해야 할 수도 있습니다.   
  
   ![PBI_SSMRP_TreeMapVisProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapvisprops.png)  
  
4. 트리 맥 시각적 개체를 선택한 상태로 왼쪽 위에서 **데이터** 탭을 선택합니다.   
  
   이제 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 가 생성한 값 및 시뮬레이션된 필드를 보고, 트리 맵에 표시되는 크기 및 색을 확인할 수 있습니다.  
  
   ![PBI_SSMRP_TreeMapDataProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapdataprops.png)  
  
6. **레이아웃** 탭을 클릭합니다.  
  
7. 트리 맵의 오른쪽 위에서 ![PBI_SSMRP_Cog](../../reporting-services/mobile-reports/media/pbi-ssmrp-cog.png) 옵션 기어를 클릭하여 포함된 메뉴를 확인합니다.   
  
   ![PBI_SSMRP_OptionsWheel](../../reporting-services/mobile-reports/media/pbi-ssmrp-optionswheel.png)  
  
8. 휠 중간에 있는 화살표를 클릭하여 닫습니다.  
  
## <a name="add-your-own-data"></a>사용자 고유의 데이터 추가  
  
1. **데이터** 탭으로 전환합니다.    
   
2. 사용자 고유의 데이터를 추가하려면 오른쪽 위에서 **데이터 추가** 를 클릭하고 데이터로 이동합니다.    
  
3. 로컬 Excel 통합 문서의 데이터를 사용할 수 있지만 이 예에서는 데이터가 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털의 공유 데이터 세트에 있습니다. "서버 추가" 메시지가 표시됩니다.  
  
4. 서버를 선택한 다음, 사용자가 만든 데이터 세트를 선택합니다.  
   
3. 다시 **데이터** 탭의 **데이터 속성** 창에서 **크기 표현**, **색 표현**및 기타 속성을 사용자 고유의 데이터에 있는 필드로 변경합니다. 
   
   *  **크기 표현**, **색 표현**및 **사용자 지정 중앙값** 은 숫자 값이 있는 필드해야 합니다. 
   *  **그룹화 방법** 은 범주이므로 텍스트 필드입니다.
   
   ![ssrs-mobile-report-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-data-properties.png)
   
6. **미리 보기** 를 선택하여 사용자 데이터로 업데이트된 트리 맵을 확인합니다.  

## <a name="add-a-gauge-to-your-mobile-report"></a>모바일 보고서에 계기 추가

게이지를 추가하여 동일한 데이터 세트로 연간 누계 판매액을 지난 해 판매액과 비교해 보겠습니다.

1. 레이아웃 탭에서 반도넛형을 캔버스로 끌어 트리 맵에 놓고 왼쪽 아래 모서리를 끌어 3x2(가로x세로) 사각형으로 만듭니다. 

2. 이번에도 시뮬레이션된 데이터로 시작합니다. 

   **시각적 개체 속성**에서 **값이 높을수록 좋음**및 **델타 레이블** 은 **대상 백분율**입니다. 변경할 수 있는 기본 **범위 중지** 가 있지만 지금은 적절합니다.

   ![ssrs-mobile-report-donut-visual-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-visual-properties.png)
   
3. **데이터** 탭에서 데이터가 있는 테이블을 선택하고 **주 값** 필드와 **비교 값**에서 비교할 필드를 선택합니다.

4. 여러 집계를 선택하여 **주 값** 과 **비교 값**각각에 대한 숫자를 지정할 수 있습니다. 이는 기본적으로 합계입니다.

   ![ssrs-mobile-report-donut-sum](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-sum.png)

5. **미리 보기** 를 선택하여 모양을 확인합니다. 

   ![ssrs-mobile-report-donut-preview](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-preview.png)

## <a name="add-a-selection-list-as-a-filter"></a>선택 목록을 필터로 추가

선택 목록은 Power BI 및 Excel에서 슬라이서와 유사하게 작동합니다. 이를 추가하여 모바일 보고서에서 다른 시각적 개체를 필터링할 수 있습니다.

1. **레이아웃** 탭에서 트리 맵의 오른쪽으로 선택 목록을 끌고 오른쪽 아래 모서리를 끌어 캔버스와 같은 높이로 2x5(가로x세로) 사각형으로 만듭니다. 

   ![ssrs-mobile-report-selection-list](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list.png)

2. **데이터** 탭의 **데이터 속성**에서 **키** 및 **레이블** 을 필터링할 데이터의 필드로 설정합니다.

   ![ssrs-mobile-report-selection-list-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list-data-properties.png)
   
## <a name="create-a-mobile-report-for-phones"></a>휴대폰용 모바일 보고서 만들기  
  
마스터 레이아웃에서 시각적 개체를 만들었으므로 이제 특별히 휴대폰 사용자용으로 최적화된 레이아웃의 모바일 보고서를 만들 수 있습니다.    
  
1. 오른쪽 위에서 캔버스 아이콘 > **전화**를 클릭합니다.  
  
2. 레이아웃 탭의 **제어 인스턴스**아래에 사용자가 만든 두 개의 차트가 표시됩니다.   
  
3. 트리 맵을 전화 캔버스로 끌어 4개의 열과 3개의 행으로 만듭니다.  
  

## <a name="save-your-mobile-report"></a>모바일 보고서 저장  
보고서를 로컬로 저장하거나 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] 웹 포털에 저장할 수 있습니다. 로컬로 저장하는 경우 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 는 캐시된 데이터와 함께 저장하므로 이를 열어 계속 작업할 수 있습니다. 하지만 모바일 디바이스에서 이를 볼 수는 없습니다.   
  
1. 왼쪽 위에서 저장 아이콘을 클릭합니다.   
   
2. 다른 사람과 공유하고 모바일 디바이스에서 보려면 **를 서버에 저장**을 클릭합니다.  
  
3. 서버에서 모바일 보고서를 저장할 폴더로 이동합니다.  
  
4. **폴더 선택** > **저장**을 클릭합니다.  
  
   보고서가 저장되었음을 확인하는 메시지가 제공됩니다.  
    
   저장한 후 포털로 돌아가면 모바일 보고서 축소판 그림이 표시됩니다.   
    
5. 웹 포털에서 보고서를 보려면 축소판 그림을 탭합니다.  
  
## <a name="view-your-report-on-the-web-portal"></a>웹 포털에서 보고서 보기

  
## <a name="view-your-report-on-a-mobile-device"></a>모바일 디바이스에서 보고서 보기   
  
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 보고서를 보려면 먼저 다음을 수행해야 합니다.

*  계정이 아직 없는 경우[Power BI 서비스에 등록](https://go.microsoft.com/fwlink/?LinkID=513879)합니다.
*  모바일 디바이스에[Power BI 모바일 앱을 다운로드](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) 합니다.  

### <a name="view-your-mobile-report"></a>모바일 보고서 보기
  
1.  모바일 디바이스에서 Power BI 앱을 열고 로그인합니다.  
    
2.  Reporting Services 모바일 보고서 및 KPI를 보려면 **Reporting Services**를 탭합니다.  
![PBI_iPad_GetStartedSm](../../reporting-services/mobile-reports/media/pbi-ipad-getstartedsm.png)  
  
3. 왼쪽 위에서 옵션 아이콘 ![PBI_iPad_OptionsIcon](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png) 을 탭하고 **서버에 연결**을 탭합니다.  
  
   ![PBI_iPad_SSMRP_ConnectCrop](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcrop.png)  
  
4. 서버의 이름을 입력하고, 서버 주소와 전자 메일 주소 및 암호를 다음 형식으로 입력합니다.  
  
   ![PBI_iPad_SSMRP_ConnectContoso](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcontoso.png)   
  
5.  이제 왼쪽 탐색 모음에 서버가 표시됩니다.  
  
    ![PBI_iPad_SSMRP_LeftNavBiggr](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-leftnavbiggr.png)  
      
> [!TIP]
> 언제든지 옵션 아이콘 ![PBI_iPad_OptionsIcon](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png)을 탭하여 Reporting Services 웹 포털의 Reporting Services 모바일 보고서와 Power BI 서비스의 대시보드 간에 이동할 수 있습니다.  

  
## <a name="view-kpis-and-mobile-reports-in-the-power-bi-app"></a>Power BI 앱에서 KPI 및 모바일 보고서 보기  
  
**KPI** 또는 **모바일 보고서** 탭을 탭합니다.   
  
![PBI_iPad_SSMRP_Portal](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-portal.png)  
  
- KPI를 탭하여 포커스 모드로 전환합니다.  
  
    ![PBI_iPad_SSMRP_Tile](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-tile.png)  
  
- 모바일 보고서를 탭하여 Power BI 앱에서 열고 상호 작용합니다.  
  
KPI와 모바일 보고서는 Reporting Services 웹 포털에 있는 것과 동일한 폴더에 표시됩니다.   
  
## <a name="see-also"></a>관련 항목:  
 
-  iOS 및 Android 디바이스용 [Power BI 모바일 앱의 온-프레미스 보고서 서버 보고서 모바일 및 KPI](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-app-ssrs-kpis-mobile-on-premises-reports) 보기
-  [Windows 10 디바이스용 Power BI 모바일 앱의 온-프레미스 보고서 서버 보고서 모바일 및 KPI](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/) 보기    
  
   

