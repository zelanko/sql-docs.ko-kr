---
title: "데이터 스트리밍 대상 구성 | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL11.DTS.DESIGNER.DATASTREAMINGDEST.F1"
ms.assetid: bcdbb833-20c8-47ff-a641-bb517f9a1af3
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# 데이터 스트리밍 대상 구성
  **고급 데이터 스트리밍 대상 편집기** 대화 상자를 사용하여 데이터 스트리밍 대상을 구성합니다. 구성 요소를 두 번 클릭하거나 데이터 흐름 디자이너에서 구성 요소를 마우스 오른쪽 단추로 클릭하고 **편집**을 클릭하여 이 대화 상자를 엽니다.  
  
 이 대화 상자에는 **구성 요소 속성**, **입력 열**, **입력 및 출력 속성**의 3개 탭이 있습니다.  
  
## 구성 요소 속성 탭  
 이 탭에는 다음과 같은 편집 가능 필드가 있습니다.  
  
|필드|Description|  
|-----------|-----------------|  
|이름|패키지에 포함된 데이터 스트리밍 대상 구성 요소의 이름입니다.|  
|ValidateExternalMetadata|디자인 타임에 외부 데이터 원본을 사용하여 구성 요소의 유효성을 검사하는지 여부를 나타냅니다. false로 설정하면 외부 데이터 원본에 대한 유효성 검사가 런타임까지 연기됩니다.|  
|IDColumnName|데이터 피드 게시 마법사가 생성한 뷰에는 이 추가 ID 열이 있습니다. 다른 응용 프로그램이 데이터를 OData 피드로 사용할 때 ID 열은 데이터 흐름의 출력 데이터에 대한 EntityKey로 사용됩니다.<br /><br /> 이 열의 기본값은 _ID입니다. ID 열에 대해 다른 이름을 지정할 수 있습니다.|  
  
## 입력 열 탭  
 이 탭의 위쪽 창에는 사용 가능한 모든 입력 열이 표시됩니다. 입력 열 중에서 이 구성 요소의 출력에 포함할 열을 선택합니다. 선택한 열은 아래쪽 창의 목록에 표시됩니다. 목록에서 **출력 별칭** 필드에 대한 새 이름을 입력해 출력 열의 이름을 변경할 수 있습니다.  
  
## 입력 및 출력 속성 탭  
 이 탭에서는 입력 열 탭에서와 비슷한 방식으로 출력 열의 이름을 변경할 수 있습니다. 왼쪽 트리 뷰에서 **데이터 스트리밍 대상 입력** 과 **입력 열**을 차례로 확장합니다. 입력 열 이름을 클릭하고 오른쪽 창에서 출력 열 이름을 변경합니다.  
  
## 관련 항목:  
 [데이터 스트리밍 대상](../../integration-services/data-flow/data-streaming-destination.md)   
 [연습: SSIS 패키지를 SQL 뷰로 게시](../../integration-services/data-flow/walkthrough-publish-an-ssis-package-as-a-sql-view.md)  
  
  