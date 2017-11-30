---
title: "데이터 집합 속성 대화 상자, 매개 변수 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
f1_keywords:
- "10150"
- sql13.rtp.rptdesigner.datasetproperties.parameters.f1
- "10023"
ms.assetid: 43b00aab-e2c3-4e85-abe1-a2b5a21efeed
caps.latest.revision: "40"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a45216068522ad248d850af14224976a8c91cadd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="dataset-properties-dialog-box-parameters"></a>데이터 집합 속성 대화 상자, 매개 변수
  **데이터 집합 속성** 대화 상자에서 **매개 변수**를 선택하여 보고서 매개 변수에 연결되는 쿼리 매개 변수를 비롯한 쿼리 매개 변수를 추가, 변경 및 삭제할 수 있습니다.  
  
 쿼리 탭에서 쿼리가 변경될 때마다 쿼리 명령이 구문 분석됩니다. 식별된 각 쿼리 매개 변수에 대해 대/소문자를 구분하는 동일한 이름의 보고서 매개 변수가 작성됩니다. 기본적으로 쿼리 매개 변수는 자동으로 쿼리 매개 변수 목록에 추가되고 해당 보고서 매개 변수에 연결됩니다.  
  
 한 보고서 매개 변수의 기본값이 쿼리 매개 변수에 연결된 다른 보고서 매개 변수에 종속된 경우 보고서 매개 변수의 순서( **보고서 매개 변수 속성** 대화 상자에 표시되는 순서)가 중요한 의미를 가집니다. 목록의 아래쪽에 있는 보고서 매개 변수는 목록의 위쪽에 있는 보고서 매개 변수를 참조할 수 있습니다. 보고서 매개 변수에 대한 자세한 내용은 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **추가**  
 목록에 새 매개 변수를 추가합니다.  
  
 **Delete**  
 선택한 매개 변수를 목록에서 제거합니다.  
  
 **매개 변수 이름**  
 **데이터 집합 속성** 대화 상자의 **쿼리** 탭에서 데이터 집합에 추가한 쿼리 매개 변수의 이름을 입력합니다.  
  
 **매개 변수 값**  
 쿼리 매개 변수의 값을 입력합니다. 이 값은 정적 값 또는 보고서 내의 개체를 참조하는 식일 수 있지만 보고서 항목이나 필드는 참조할 수 없습니다. 기본적으로 **값** 에는 보고서 매개 변수를 가리키는 식이 포함됩니다.  
  
 **위쪽 화살표**  
 선택한 매개 변수를 목록에서 위쪽으로 이동합니다.  
  
 **아래쪽 화살표**  
 선택한 매개 변수를 목록에서 아래쪽으로 이동합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [보고서 매개 변수&#40;보고서 작성기 및 보고서 디자이너&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [보고서 데이터 집합&#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [보고서 매개 변수의 순서 변경&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)  
  
  
