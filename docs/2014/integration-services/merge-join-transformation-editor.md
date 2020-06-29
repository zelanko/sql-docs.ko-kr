---
title: 병합 조인 변환 편집기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b74b8cd3e010f372cf0c0a50f5c0e19054924d0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424600"
---
# <a name="merge-join-transformation-editor"></a>병합 조인 변환 편집기
  **병합 조인 변환 편집기** 대화 상자를 사용하여 조인 유형, 조인 열 및 조인으로 결합된 두 입력을 병합하기 위한 출력 열을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  병합 조인 변환에는 정렬된 데이터를 입력해야 합니다. 이러한 중요 요구 사항에 대한 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
 병합 조인 변환에 대한 자세한 내용은 [Merge Join Transformation](data-flow/transformations/merge-join-transformation.md)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **조인 유형**  
 내부 조인, 왼쪽 우선 외부 조인 또는 완전 조인을 사용할지 여부를 지정합니다.  
  
 **입력 바꾸기**  
 **입력 바꾸기** 단추를 사용하여 입력 간에 순서를 바꿉니다. 왼쪽 우선 외부 조인 옵션과 함께 사용하면 유용합니다.  
  
 **입력**  
 먼저 사용 가능한 입력 목록에서 병합된 출력에 포함할 각 열에 대한 입력을 선택합니다.  
  
 입력은 별도의 두 테이블에 따로 표시됩니다. 출력에 포함할 열을 선택합니다. 열을 끌어 테이블 간에 조인을 만듭니다. 조인을 삭제하려면 조인을 선택한 다음 Delete 키를 누릅니다.  
  
 **입력 열**  
 선택한 입력의 사용 가능한 열 목록에서 병합 출력에 포함할 열을 선택합니다.  
  
 **출력 별칭**  
 각 출력 열의 별칭을 입력합니다. 기본값은 입력 열의 이름이지만 설명이 포함된 고유 이름을 임의로 선택할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [병합 및 병합 조인 변환에 대 한 데이터 정렬](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [병합 조인 변환을 사용 하 여 데이터 집합 확장](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [병합 변환](data-flow/transformations/merge-transformation.md)   
 [UNION ALL 변환](data-flow/transformations/union-all-transformation.md)  
  
  
