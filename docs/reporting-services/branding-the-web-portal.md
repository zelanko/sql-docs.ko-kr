---
title: "웹 포털 브랜딩 | Microsoft Docs"
ms.custom: ""
ms.date: "07/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6dac97f7-02a6-4711-81a3-e850a6b40bf1
caps.latest.revision: 8
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 8
---
# 웹 포털 브랜딩
웹 포털을 비즈니스로 브랜딩하여 모양을 변경할 수 있습니다. 이 작업은 브랜드 패키지를 통해 수행합니다. 브랜드 패키지는 사용자가 CSS 스타일 시트에 대한 깊은 지식이 없어도 웹 포털을 만들 수 있도록 설계되었습니다.  
  
항목 내용  
  
-   [브랜드 패키지 만들기](#create)  
  
-   [웹 포털에 브랜드 패키지 적용](#apply)  
  
-   [metadata.xml 예제](#metadata)  
  
-   [colors.json 예제](#colors)  
  
<iframe width="560" height="315" src="https://www.youtube.com/embed/m08kLuofwFA?list=PLv2BtOtLblH3F--8WmK9QcLbx6dV_lVkL" frameborder="0" allowfullscreen></iframe>  
  
<a name="create">  
## 브랜드 패키지 만들기  
  
Reporting Services의 브랜드 패키지는 3개 항목으로 구성되어 있으며 zip 파일로 패키지화되어 있습니다.   
  
- color.json  
- metadata.xml  
- logo.png(옵션)  
  
파일 이름은 위와 동일해야 하며 zip 파일은 원하는 대로 정할 수 있습니다.  
  
### metadata.xml  
  
metadata.xml 파일을 사용하면 브랜드 패키지의 이름을 설정할 수 있으며 이 파일에는 colors.json 및 logo.png 파일에 대한 참조 항목이 있습니다.  
  
브랜드 패키지의 이름을 변경하려면 **SystemResourcePackage** 요소의 **이름** 특성을 변경합니다.  
  
    name="Multicolored example brand"  
  
브랜드 패키지에 로고 사진을 포함할 수도 있습니다. 이 항목은 Contents 요소 안에 나열됩니다.  
  
로고가 없는 예제  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
    </Contents>  
  
로고가 있는 예제  
  
    <Contents>  
      <Item key="colors" path="colors.json" />  
      <Item key="logo" path="logo.png" />  
    </Contents>  
  
### Colors.json  
  
브랜드 패키지가 업로드되면 서버가 colors.json에서 적절한 이름/값 쌍을 추출하고 마스터 LESS 스타일시트인 brand.less로 병합합니다. 그런 다음 이 LESS 파일이 처리되고 결과 CSS 파일이 클라이언트에 제공됩니다. 스타일시트의 모든 색은 16진수의 6자 색 표현을 따릅니다.  
  
LESS 스타일시트에는 다음과 같이 사전 정의된 LESS 변수를 참조하는 블록이 포함되어 있습니다.  
  
    /* primary buttons */   
    .btn-primary {   
        color:@primaryButtonColor;   
        background-color:@primaryButtonBg;   
    }  
  
이 스타일시트가 CSS 구문과 유사하긴 하지만 @기호의 접두사가 포함된 색 값은 LESS에만 해당합니다. 이러한 색 값은 json 파일에서 해당 값을 설정하는 변수입니다.  
  
예를 들어 colors.json 파일의 값이 다음과 같은 경우  
  
    "primary":"#009900",   
    "primaryContrast":"#ffffff"   
  
처리된 출력은 **@primaryButtonBg** LESS 변수를 조회하고 **primary**라고 하는 json 속성(이 예제의 경우 #009900)으로 매핑된 것을 확인할 수 있습니다. 따라서 올바른 CSS가 출력됩니다.  
  
    .btn-primary {   
        color:#ffffff;   
        background-color:#009900;   
    }  
  
모든 기본 단추는 어두운 녹색 바탕에 흰색 텍스트로 렌더링됩니다.  
  
Reporting Services의 colors.json 파일에는 항목이 그룹화되는 두 가지 기본 범주가 있습니다.  
  
- **인터페이스**: Reporting Services 웹 포털에만 해당하는 항목이 포함됩니다.  
- **테마**: 만들고 있는 모바일 보고서에만 해당하는 항목이 포함됩니다.  
  
인터페이스 섹션은 다음 그룹으로 나누어집니다.  
  
|섹션|Description|  
|---|---|  
|primary|단추 및 가리킨 항목 색|  
|보조|제목 표시줄, 검색 표시줄, 왼쪽 메뉴(표시된 경우), 해당 항목의 텍스트 색|  
|중립 기본|홈 및 보고서 영역 배경|  
|중립 보조|텍스트 상자 및 폴더 옵션 배경, 설정 메뉴|  
|중립 3차|사이트 설정 배경|  
|위험/경고/성공 메시지|이러한 메시지의 색|  
|KPI|양호(1), 중립(0), 중립(-1), 없음의 색을 관리합니다.|  
  
모바일 보고서 게시자를 사용하여 브랜드 패키지가 배포된 서버에 처음으로 연결하면 테마가 응용 프로그램의 오른쪽 위에서 사용할 수 있는 테마에 추가됩니다.  
  
![ssRSBrandingMobileReportPublisher](../reporting-services/media/ssrsbrandingmobilereportpublisher.png)  
  
그러면 테마를 배포한 서버와 동일한 서버용이 아닐 경우에도 사용자가 작성하는 모바일 보고서에 해당 테마를 사용할 수 있습니다.   
  
### 로고 사용  
  
브랜드 패키지를 사용하여 로고를 포함할 경우 사이트 설정 메뉴에서 웹 포털에 대해 설정한 이름 위치 대신 웹 포털에 표시됩니다.  
  
로고에 포함하는 파일은 PNG 파일 형식을 사용해야 합니다. 파일을 서버에 업로드하면 크기가 조정되며 약 290px x 60px로 조정됩니다.  
  
<a name="apply">  
## 웹 포털에 브랜드 패키지 적용  
  
브랜드 패키지를 추가, 다운로드, 제거하려면 다음을 수행할 수 있습니다.  
  
1.  오른쪽 상단에서 **기어 모양** 을 선택합니다.  
  
2.  **사이트 설정**을 선택합니다.  
  
    ![ssRSGearMenu](../reporting-services/media/ssrsgearmenu.png)  
  
3.  **브랜딩**을 선택합니다.  
  
    ![ssRSBranding](../reporting-services/media/ssrsbranding.png)  
  
**현재 설치된 브랜드 패키지** 에 업로드된 패키지의 이름이 표시되거나 없음이 표시됩니다.  
  
**브랜드 패키지 업로드** 가 웹 포털에 패키지를 적용합니다. 즉시 적용되는 것을 확인할 수 있습니다.  
  
패키지를 **다운로드** 또는 **제거** 할 수도 있습니다. 패키지를 제거하면 웹 포털이 즉시 기본 브랜드로 재설정됩니다.  
  
<a name="metadata">  
## metadata.xml 예제  
  
    \<?xml version="1.0" encoding="utf-8"?>  
    <SystemResourcePackage xmlns="http://schemas.microsoft.com/sqlserver/reporting/2016/01/systemresourcepackagemetadata"  
        type="UniversalBrand"  
        version="2.0.2"  
        name="Multicolored example brand"  
        >  
        <Contents>  
            <Item key="colors" path="colors.json" />  
            <Item key="logo" path="logo.png" />  
        </Contents>  
    </SystemResourcePackage>  
  
<a name="colors">  
## Colors.json 예제  
  
    {  
        "name":"Multicolored example brand",  
        "version":"1.0",  
        "interface":{  
            "primary":"#b31e1e",  
            "primaryAlt":"#ca0806",  
            "primaryAlt2":"#621013",  
            "primaryAlt3":"#e40000",  
            "primaryAlt4":"#e14e50",  
            "primaryContrast":"#fff",  
  
            "secondary":"#042200",  
            "secondaryAlt":"#0f4400",  
            "secondaryAlt2":"#155500",  
            "secondaryAlt3":"#217700",  
            "secondaryContrast":"#49e63c",  
  
            "neutralPrimary":"#d8edff",  
            "neutralPrimaryAlt":"#c9e6ff",  
            "neutralPrimaryAlt2":"#aedaff",  
            "neutralPrimaryAlt3":"#88c8ff",  
            "neutralPrimaryContrast":"#0a2b4c",  
  
            "neutralSecondary":"#e9d8eb",  
            "neutralSecondaryAlt":"#d9badc",  
            "neutralSecondaryAlt2":"#b06cb5",  
            "neutralSecondaryAlt3":"#a75bac",  
            "neutralSecondaryContrast":"#250a26",  
  
            "neutralTertiary":"#f79220",  
            "neutralTertiaryAlt":"#f8a54b",  
            "neutralTertiaryAlt2":"#facc9b",  
            "neutralTertiaryAlt3":"#fce3c7",  
            "neutralTertiaryContrast":"#391d00",  
  
            "danger":"#ff0000",  
            "success":"#00ff00",  
            "warning":"#ff8800",  
            "info":"#00ff",  
            "dangerContrast":"#fff",  
            "successContrast":"#fff",  
            "warningContrast":"#fff",  
            "infoContrast":"#fff",  
  
            "kpiGood":"#4fb443",  
            "kpiBad":"#de061a",  
            "kpiNeutral":"#d9b42c",  
            "kpiNone":"#333",  
            "kpiGoodContrast":"#fff",  
            "kpiBadContrast":"#fff",  
            "kpiNeutralContrast":"#fff",  
            "kpiNoneContrast":"#fff"  
           },  
           "theme":{  
            "dataPoints":[  
                "#0072c6",  
                "#f68c1f",  
                "#269657",  
                "#dd5900",  
                "#5b3573",  
                "#22bdef",  
                "#b4009e",  
                "#008274",  
                "#fdc336",  
                "#ea3c00",  
                "#00188f",  
                "#9f9f9f"  
            ],  
  
            "good":"#85ba00",  
            "bad":"#e90000",  
            "neutral":"#edb327",  
            "none":"#333",  
  
            "background":"#fff",  
            "foreground":"#222",  
            "mapBase":"#00aeef",  
            "panelBackground":"#f6f6f6",  
            "panelForeground":"#222",  
            "panelAccent":"#00aeef",  
            "tableAccent":"#00aeef",  
  
            "altBackground":"#f6f6f6",  
            "altForeground":"#000",  
            "altMapBase":"#f68c1f",  
            "altPanelBackground":"#235378",  
            "altPanelForeground":"#fff",  
            "altPanelAccent":"#fdc336",  
            "altTableAccent":"#fdc336"  
        }  
    }  
  
  
  
  
  
  
  
  
  
