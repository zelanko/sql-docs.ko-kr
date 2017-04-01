---
title: "보고서 모델 쿼리 디자이너 사용자 인터페이스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "10015"
  - "sql13.rtp.rptdesigner.dataview.smqlquerydesigner.f1"
helpviewer_keywords: 
  - "보고서 모델 [Reporting Services], 쿼리"
  - "데이터 집합 [Reporting Services], 만들기"
  - "쿼리 디자이너 [Reporting Services]"
ms.assetid: db86c208-ff1e-4297-aa0c-c250f053f83e
caps.latest.revision: 31
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 31
---
# 보고서 모델 쿼리 디자이너 사용자 인터페이스
  보고서 디자이너는 보고서에 사용할 보고서 서버 모델 데이터 원본의 데이터를 지정할 수 있는 두 가지 쿼리 디자이너를 제공합니다. 그래픽 쿼리 디자이너를 사용하여 모델 엔터티와 엔터티 필드를 탐색하고 선택할 수 있습니다. 또한 텍스트 기반 쿼리 디자이너를 사용하여 XML 형식으로 SMDL(Semantic Model Definition Language) 사양에서 직접 작업할 수 있습니다.  
  
> [!IMPORTANT]  
>  사용자는 쿼리를 작성하고 실행할 때 데이터 원본에 액세스합니다. 데이터 원본에 대해서는 읽기 전용 권한과 같이 최소한의 사용 권한을 부여해야 합니다.  
  
## 그래픽 쿼리 디자이너  
 보고서 디자이너는 보고서 처리 중 보고서 데이터 집합에 대한 필드 컬렉션을 채우는 SMDL 쿼리를 디자인 및 실행하는 데 사용할 수 있는 그래픽 쿼리 디자이너를 제공합니다. 그래픽 쿼리 디자이너는 3개의 영역 또는 창으로 구분됩니다.  
  
 다음 그림에서는 레이블과 함께 각 창을 보여 줍니다.  
  
 ![의미 체계 모델 쿼리 디자이너 UI](../../reporting-services/report-data/media/rsqd-dsawmodel-smql.gif "의미 체계 모델 쿼리 디자이너 UI")  
  
 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|함수|  
|----------|--------------|  
|탐색기 창|모델의 엔터티 및 엔터티 필드를 그래픽으로 표시합니다. 이 창을 사용하여 엔터티, 관련 엔터티 및 필드를 탐색할 수 있습니다.|  
|디자인 영역|모델의 필드 목록을 표시합니다. 이 창을 사용하여 선택한 필드의 레이아웃을 정렬할 수 있습니다.|  
|결과 창|쿼리 결과를 표시합니다. 쿼리를 실행하려면 아무 창이나 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭하거나 도구 모음에서 **실행**(![쿼리 실행](../../reporting-services/report-data/media/rsqdicon-run.png "쿼리 실행")) 단추를 클릭합니다.|  
  
 탐색기 또는 디자인 영역 창에서 정보를 변경하면 **실행**을 클릭했을 때 결과 창의 내용이 영향을 받습니다.  
  
 디자인 영역에서 열을 삭제하는 것과 같이 특정 창 내에서 동작을 수행하려면 열을 마우스 오른쪽 단추로 클릭한 다음 메뉴에서 명령을 클릭합니다.  
  
### 그래픽 쿼리 디자이너 도구 모음  
 쿼리를 디자인할 때 도구 모음 단추를 사용할 수도 있습니다. 다음 표에서는 도구 모음의 단추와 해당 기능을 보여 줍니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다. 보고서 서버 모델 데이터 원본에 대한 쿼리는 XML 형식의 SMQL(Semantic Model Query Language) 사양입니다.|  
|**가져오기**|파일 시스템의 보고서 정의 파일(.rdl)에서 기존 쿼리를 가져옵니다. 자세한 내용은 [보고서 포함된 데이터 집합 및 공유 데이터 집합&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.|  
|![동작 실행 취소](../../reporting-services/report-data/media/rsqdicon-undo.png "동작 실행 취소")|마지막 동작 실행을 취소합니다.|  
|![동작 다시 실행](../../reporting-services/report-data/media/rsqdicon-redo.png "동작 다시 실행")|마지막 동작을 다시 실행합니다.|  
|![쿼리 실행](../../reporting-services/report-data/media/rsqdicon-run.png "쿼리 실행")|쿼리를 실행하고 결과 창에 결과 행을 표시합니다.|  
|![선택한 필터 열 옆에 있는 필터 그래픽](../../reporting-services/report-data/media/rsqdicon-filter.png "선택한 필터 열 옆에 있는 필터 그래픽")|필터링할 데이터를 지정할 수 있는 **데이터 필터링** 대화 상자를 엽니다. 디자인 영역에 있는 데이터와 무관하게 필터를 지정할 수 있습니다.|  
  
## 텍스트 기반 쿼리 디자이너  
 보고서 서버 모델 데이터 집합 쿼리를 만들 경우 그래픽 쿼리 디자이너가 기본적으로 표시됩니다. 텍스트 기반 쿼리 디자이너로 전환하려면 도구 모음에서 **텍스트로 편집** 토글 단추를 클릭합니다.  
  
 텍스트 기반 쿼리 디자이너는 SMQL 쿼리 창과 결과 창의 두 가지 창으로 구성되어 있습니다. 다른 원본의 SMQL 쿼리 사양을 이미 갖고 있으며 이를 쿼리 창에 붙여넣고 싶은 경우에 주로 이 쿼리 디자이너 뷰가 사용됩니다. 그래픽 쿼리 디자이너와 달리 텍스트 기반 쿼리 디자이너는 쿼리 구문을 확인하거나 쿼리를 재구성하지 않습니다. 도구 모음에서 **실행** 을 클릭할 경우 데이터 원본에서 쿼리가 실행되고 결과 창에 결과가 표시됩니다.  
  
 다음 그림에서는 레이블과 함께 각 창을 보여 줍니다.  
  
 ![일반 의미 체계 모델 언어 쿼리 디자이너](../../reporting-services/report-data/media/rsqd-dsawmodel-smql-generic.gif "일반 의미 체계 모델 언어 쿼리 디자이너")  
  
 다음 표에서는 각 창의 기능을 설명합니다.  
  
|창|함수|  
|----------|--------------|  
|쿼리 창|SMQL 사양 텍스트를 표시합니다.|  
|결과 창|쿼리 결과를 표시합니다. 쿼리를 실행하려면 아무 창이나 마우스 오른쪽 단추로 클릭한 다음 **실행**을 클릭하거나 도구 모음에서 **실행** 단추를 클릭합니다.|  
  
### 텍스트 기반 쿼리 디자이너 도구 모음  
 쿼리를 디자인할 때 도구 모음 단추를 사용할 수도 있습니다. 다음 표에서는 도구 모음의 단추와 해당 기능을 보여 줍니다.  
  
|단추|Description|  
|------------|-----------------|  
|**텍스트로 편집**|텍스트 기반 쿼리 디자이너와 그래픽 쿼리 디자이너 사이를 전환합니다.|  
|**가져오기**|기존 보고서에서 쿼리를 가져옵니다.|  
|![쿼리 실행](../../reporting-services/report-data/media/rsqdicon-run.png "쿼리 실행")|쿼리 텍스트를 실행하고 결과 창에 결과 행 집합을 표시합니다.|  
  
## 관련 항목:  
 [쿼리 디자인 도구&#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [외부 데이터 원본의 데이터 추가&#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)   
 [보고서 모델 연결&#40;SSRS&#41;](../../reporting-services/report-data/report-model-connection-ssrs.md)   
 [RSReportDesigner 구성 파일](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)  
  
  