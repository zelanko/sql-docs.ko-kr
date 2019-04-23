---
title: 데이터 집합 속성 대화 상자, 필드 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasetproperties.fields.f1
- "10140"
ms.assetid: e1367556-736e-4a6b-b9e7-10432a3e50b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b1c49beb22a3a91e3d42aa7ce4ed99b5e107b4d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59956929"
---
# <a name="dataset-properties-dialog-box-fields"></a>데이터 세트 속성 대화 상자, 필드
  **데이터 집합 속성** 대화 상자에서 **필드** 를 선택하여 보고서 데이터 집합의 필드 컬렉션을 변경할 수 있습니다. 필드 목록은 자동으로 채워지지만 **필드** 를 사용하여 쿼리와 계산 필드를 추가, 편집 및 삭제할 수도 있습니다.  
  
## <a name="options"></a>변수  
 **추가**  
 데이터 세트에 새 쿼리 필드나 계산 필드를 추가합니다.  
  
 **Delete**  
 선택한 필드를 데이터 세트에서 삭제합니다.  
  
 **필드 이름**  
 필드의 이름을 입력합니다. 필드는 데이터 세트 내에서 고유해야 합니다. 데이터 세트 쿼리의 기존 필드에 대해서는 각각 이름이 미리 채워집니다.  
  
 **필드 원본**  
 필드의 값을 입력합니다.  
  
 계산 필드의 경우 필드 원본은 데이터 세트 쿼리 또는 사용자가 만든 식으로 검색된 기존 필드의 이름이어야 합니다. 예를 들어 Sales라는 쿼리 필드의 값에 10을 곱한 값을 표시하는 필드를 만들려면 `=10 * Fields!Sales.Value`식을 사용합니다.  
  
 쿼리 필드의 경우 필드 원본은 데이터 세트 쿼리로 검색된 기존 필드의 이름이어야 합니다.  
  
 **식 (fx)**  
 계산 필드의 식을 추가하거나 변경합니다. 이 단추는 **추가** 를 클릭하고 **계산 필드**를 선택했을 때만 나타납니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 집합 필드 컬렉션&#40;보고서 작성기 및 SSRS&#41;](report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [보고서에 데이터 추가 &#40;보고서 작성기 및 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [식&#40;보고서 작성기 및 SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
