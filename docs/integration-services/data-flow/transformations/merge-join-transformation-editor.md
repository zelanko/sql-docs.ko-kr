---
title: "병합 조인 변환 편집기 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6bba110363b36294a67880f3efbdec52e1c6db0d
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="merge-join-transformation-editor"></a>병합 조인 변환 편집기
  **병합 조인 변환 편집기** 대화 상자를 사용하여 조인 유형, 조인 열 및 조인으로 결합된 두 입력을 병합하기 위한 출력 열을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  병합 조인 변환에는 정렬된 데이터를 입력해야 합니다. 이러한 중요 요구 사항에 대한 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
 병합 조인 변환에 대한 자세한 내용은 [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **조인 유형**  
 내부 조인, 왼쪽 우선 외부 조인 또는 완전 조인을 사용할지 여부를 지정합니다.  
  
 **입력 바꾸기**  
 **입력 바꾸기** 단추를 사용하여 입력 간에 순서를 바꿉니다. 왼쪽 우선 외부 조인 옵션과 함께 사용하면 유용합니다.  
  
 **Input**  
 먼저 사용 가능한 입력 목록에서 병합된 출력에 포함할 각 열에 대한 입력을 선택합니다.  
  
 입력은 별도의 두 테이블에 따로 표시됩니다. 출력에 포함할 열을 선택합니다. 열을 끌어 테이블 간에 조인을 만듭니다. 조인을 삭제하려면 조인을 선택한 다음 Delete 키를 누릅니다.  
  
 **입력 열**  
 선택한 입력의 사용 가능한 열 목록에서 병합 출력에 포함할 열을 선택합니다.  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)   
 [병합 및 병합 조인 변환을 위한 데이터 정렬](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [병합 조인 변환을 사용 하 여 데이터 집합을 확장 합니다.](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [병합 변환](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Union All 변환](../../../integration-services/data-flow/transformations/union-all-transformation.md)  
  
  
