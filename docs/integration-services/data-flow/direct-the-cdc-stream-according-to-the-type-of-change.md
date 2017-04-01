---
title: "변경 유형에 따라 CDC 스트림 전송 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3afa531e-f425-40a4-a1bf-1c3e1727287e
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# 변경 유형에 따라 CDC 스트림 전송
  CDC 분할자 변환을 추가 및 구성하려면 패키지에 적어도 하나 이상의 데이터 흐름 태스크와 하나의 CDC 원본이 들어 있어야 합니다.  
  
 패키지에 추가되는 CDC 원본에는 NetCDC 처리 모드가 선택되어 있어야 합니다. 처리 모드 선택에 대한 자세한 내용은 [CDC 원본 편집기&#40;연결 관리자 페이지&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)를 참조하세요.  
  
### 변경 유형에 따라 CDC 스트림을 전송하려면  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 원하는 패키지가 들어 있는 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  **데이터 흐름** 탭을 클릭한 다음 **도구 상자**에서 CDC 분할자를 디자인 화면으로 끌어 옵니다.  
  
4.  패키지에 포함된 CDC 원본을 CDC 분할자에 연결합니다.  
  
5.  하나 이상의 대상에 CDC 분할자를 연결합니다. 최대 3개의 다른 출력을 연결할 수 있습니다.  
  
6.  다음 출력 중 하나를 선택합니다.  
  
    -   삭제 출력: 삭제 변경 행이 전송되는 출력입니다.  
  
    -   삽입 출력: 삽입 변경 행이 전송되는 출력입니다.  
  
    -   업데이트 출력: 업데이트 전/후 변경 행 및 병합 변경 행이 전송되는 출력입니다.  
  
7.  필요에 따라 **고급 편집기** 대화 상자를 사용하여 고급 속성을 구성할 수도 있습니다.  
  
     **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 포함됩니다.  
  
     **고급 편집기** 대화 상자를 열려면  
  
    -   **프로젝트의** 데이터 흐름 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 화면에서 CDC 분할자를 마우스 오른쪽 단추로 클릭하고 **고급 편집기 표시**를 선택합니다.  
  
     CDC 분할자 사용에 대한 자세한 내용은 Microsoft SQL Server Integration Services용 CDC 구성 요소를 참조하십시오.  
  
## 관련 항목:  
 [CDC 분할자](../../integration-services/data-flow/cdc-splitter.md)  
  
  