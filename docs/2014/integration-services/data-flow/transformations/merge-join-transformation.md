---
title: 병합 조인 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0620aec0c710e513115455388276c72cc4371e9a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48171045"
---
# <a name="merge-join-transformation"></a>Merge Join Transformation
  병합 조인 변환은 FULL, LEFT 또는 INNER 조인으로 두 개의 정렬된 데이터 세트를 조인하여 생성된 출력을 제공합니다. 예를 들어 LEFT 조인을 사용하여 제품 정보가 포함된 테이블을 제품 제조 국가/지역이 나열된 테이블과 조인할 수 있습니다. 조인 결과로 모든 제품과 제조 국가/지역이 나열된 테이블이 생성됩니다.  
  
 다음과 같은 방법으로 병합 조인 변환을 구성할 수 있습니다.  
  
-   조인이 FULL, LEFT 또는 INNER 조인인지 지정합니다.  
  
-   조인에 사용되는 열을 지정합니다.  
  
-   변환에서 Null 값을 다른 Null과 같은 값으로 처리할지를 지정합니다.  
  
    > [!NOTE]  
    >  Null 값이 같은 값으로 처리되지 않는 경우 이 변환은 SQL Server 데이터베이스 엔진과 동일한 방식으로 Null 값을 처리합니다.  
  
 이 변환에는 두 개의 입력과 하나의 출력이 있습니다. 오류 출력은 지원하지 않습니다.  
  
## <a name="input-requirements"></a>입력 요구 사항  
 병합 조인 변환에는 정렬된 데이터를 입력해야 합니다. 이러한 중요 요구 사항에 대한 자세한 내용은 [병합 및 병합 조인 변환을 위한 데이터 정렬](sort-data-for-the-merge-and-merge-join-transformations.md)을 참조하세요.  
  
## <a name="join-requirements"></a>조인 요구 사항  
 병합 조인 변환을 사용하려면 조인된 열에 일치하는 메타데이터가 있어야 합니다. 예를 들어 숫자 데이터 형식의 열을 문자 데이터 형식의 열과 조인할 수는 없습니다. 데이터가 문자열 데이터 형식이면 두 번째 입력의 열 길이는 함께 병합될 첫 번째 입력의 열 길이보다 작거나 같아야 합니다.  
  
## <a name="buffer-throttling"></a>버퍼 스로틀  
 값을 구성할 필요가 없습니다를 `MaxBuffersPerInput` 속성 Microsoft 변경 된 병합 조인 변환에서 과도 한 메모리를 사용할 위험을 줄이는 때문입니다. 과도한 메모리가 사용되는 문제는 여러 병합 조인 입력에서 균일하지 않은 속도로 데이터를 생성하는 경우에 발생합니다.  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 이 변환의 속성 설정 방법을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [병합 조인 변환을 사용하여 데이터 집합 확장](merge-join-transformation.md)  
  
-   [데이터 흐름 구성 요소의 속성 설정](../set-the-properties-of-a-data-flow-component.md)  
  
-   [병합 및 병합 조인 변환을 위한 데이터 정렬](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>관련 항목  
 [병합 조인 변환 편집기](../../merge-join-transformation-editor.md)   
 [병합 변환](merge-transformation.md)   
 [Union All 변환](union-all-transformation.md)   
 [Integration Services 변환](integration-services-transformations.md)  
  
  
