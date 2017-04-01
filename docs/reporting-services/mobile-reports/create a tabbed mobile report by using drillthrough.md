---
title: "드릴스루를 사용하여 탭으로 구성된 모바일 보고서 만들기 | Reporting Services 모바일 보고서 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 드릴스루를 사용하여 탭으로 구성된 모바일 보고서 만들기 | Reporting Services 모바일 보고서
드릴스루 보고서 및 매개 변수를 사용하여 탭으로 구성된 보고서 모양으로 작업되는 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 모바일 보고서를 만드는 방법에 대해 알아봅니다.

예를 들어 이 보고서의 위쪽에는 탭 역할을 하는 계기가 있습니다. 운송 계기를 클릭하면 차트의 나머지 부분에서 데이터가 운송 데이터로 필터링됩니다.

![06-모바일-보고서-웹-뷰어-운송](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

백그라운드에서 이는 실제로 별개의 보고서 5개로 구성된 집합이며 각 보고서는 보고서 맨 위에서 선택한 계기와 일치하도록 보고서를 필터링하는 서로 다른 매개 변수를 포함합니다. 

이 예제에서는 먼저 5개의 보고서를 만든 다음 5개 보고서 각각에 대해 다른 4개 계기가 다른 4개 보고서로 드릴스루되도록 만듭니다. 

다음은 단계를 간략하게 설명한 것입니다.

1. 다음 5개의 계기가 포함된 판매라는 보고서를 만듭니다.
     - Sales
     - 운송
     - 연료
     - 저장소
     - 기타 비용
2. 다음과 같은 보고서 복사본 4개를 만듭니다. 
     - 운송
     - 연료
     - 저장소
     - 기타 비용
3.  판매 보고서에서 각 보고서로의 드릴스루로 4개 계기(판매 계기 제외)를 각각 설정합니다.

4. 계속 판매 보고서에서 판매 계기의 강조 속성을 보고서의 나머지 부분과 대비되도록 설정하여 눈에 띄게 합니다.

5.  이제 운송 보고서에서 판매 계기를 판매 보고서에 대한 드릴스루로 설정하고 다른 3개 계기를 각 보고서로의 드릴스루로 설정합니다.

6. 계속 운송 보고서에서 운송 계기의 강조 속성을 보고서의 나머지 부분과 대비되도록 설정합니다.

5. 연료, 저장소 및 기타 비용 보고서에 대해 반복합니다. 







  
