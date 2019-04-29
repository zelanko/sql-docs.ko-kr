---
title: 복합 도메인에 열 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9422412-8a3d-45ae-af7f-072c902a09ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9ce189688bd33f3cb63280e4fa44bb2284ee9e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900039"
---
# <a name="map-columns-to-composite-domains"></a>복합 도메인에 열 매핑
  복합 도메인은 둘 이상의 단일 도메인으로 구성됩니다. 여러 개의 열을 이 도메인에 매핑하거나 구분된 값이 포함된 단일 열을 이 도메인에 매핑할 수 있습니다.  
  
 열이 여러 개 있는 경우 각 열을 복합 도메인의 각 단일 도메인에 매핑하여 데이터 정리에 복합 도메인 규칙을 적용해야 합니다. Data Quality 클라이언트에서 복합 도메인에 포함된 단일 도메인을 선택합니다. 자세한 내용은 [복합 도메인 만들기](../../../data-quality-services/create-a-composite-domain.md)을 참조하세요.  
  
 구분된 값을 가진 단일 열이 있으면 이 단일 열을 복합 도메인에 매핑해야 합니다. 값은 단일 도메인이 복합 도메인에 나타나는 순서와 동일한 순서로 나타나야 합니다. 데이터 원본의 구분 기호는 복합 도메인 값을 구문 분석하는 데 사용되는 구분 기호와 일치해야 합니다. Data Quality 클라이언트에서 복합 도메인의 구분 기호를 선택하고 다른 속성도 설정합니다. 자세한 내용은 [복합 도메인 만들기](../../../data-quality-services/create-a-composite-domain.md)을 참조하세요.  
  
### <a name="to-map-multiple-columns-to-a-composite-domain"></a>여러 개의 열을 복합 도메인에 매핑하려면  
  
1.  DQS 정리 변환을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
2.  **연결 관리자** 탭에서 복합 도메인이 사용 가능한 도메인 목록에 나타나는지 확인합니다.  
  
3.  **매핑** 탭의 **사용 가능한 입력 열** 영역에서 열을 선택합니다.  
  
4.  **입력 열** 필드의 각 열에 대해 **도메인** 필드에서 단일 도메인을 선택합니다. 복합 도메인에 속해 있는 단일 도메인만 선택할 수 있습니다.  
  
5.  필요에 따라 **원본 별칭**, **출력 별칭**및 **상태 별칭** 필드에 나타나는 이름을 수정합니다.  
  
6.  필요에 따라 **고급** 탭에서 속성을 설정합니다. 속성에 대한 자세한 내용은 [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md)를 참조하십시오.  
  
### <a name="to-map-a-column-with-delimited-values-to-a-composite-domain"></a>구분된 값을 가진 열을 복합 도메인에 매핑하려면  
  
1.  DQS 정리 변환을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 클릭합니다.  
  
2.  **연결 관리자** 탭에서 복합 도메인이 사용 가능한 도메인 목록에 나타나는지 확인합니다.  
  
3.  **매핑** 탭의 **사용 가능한 입력 열** 영역에서 열을 선택합니다.  
  
4.  **입력 열** 필드의 열에 대해 **도메인** 필드에서 복합 도메인을 선택합니다.  
  
5.  필요에 따라 **원본 별칭**, **출력 별칭**및 **상태 별칭** 필드에 나타나는 이름을 수정합니다.  
  
6.  필요에 따라 **고급** 탭에서 속성을 설정합니다. 속성에 대한 자세한 내용은 [DQS Cleansing Transformation Editor Dialog Box](../../dqs-cleansing-transformation-editor-dialog-box.md)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [DQS 정리 변환](dqs-cleansing-transformation.md)  
  
  
