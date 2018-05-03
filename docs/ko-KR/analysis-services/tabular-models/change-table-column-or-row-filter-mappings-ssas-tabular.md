---
title: 테이블, 열 또는 행 필터 매핑 변경 | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2124c526-5772-4f84-a019-9dd3e906e8dd
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d7c2ec71bb6fe0703e374c105bcb106785a28657
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="change-table-column-or-row-filter-mappings"></a>테이블, 열 또는 행 필터 매핑 변경 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  이 문서를 사용 하 여 테이블, 열 또는 행 필터 매핑을 변경 하는 방법에 설명 된 **테이블 속성 편집** 대화 상자에서 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]합니다.  
  
 **테이블 속성 편집** 대화 상자의 옵션은 원래 데이터를 가져올 때 목록에서 테이블을 선택하는 방법을 사용했는지 아니면 SQL 쿼리를 사용하는 방법을 사용했는지에 따라 다릅니다. 목록에서 선택하여 데이터를 가져온 경우 **테이블 속성 편집** 대화 상자에 테이블 미리 보기 모드가 표시됩니다. 이 모드에서는 원본 테이블의 첫 50개 행으로 제한된 하위 집합만 표시됩니다. SQL 문을 사용하여 데이터를 가져온 경우 **테이블 속성 편집** 대화 상자에 SQL 문만 표시됩니다. SQL 쿼리 문을 사용하면 필터를 디자인하거나 SQL 문을 직접 편집하여 행의 일부만 검색할 수 있습니다.  
  
 현재 테이블과 다른 열이 있는 테이블로 원본을 변경하면 열이 다르다는 경고 메시지가 표시됩니다. 그런 다음 현재 테이블에 넣을 열을 선택하고 **저장**을 클릭합니다. 테이블 왼쪽의 확인란을 선택하여 테이블 전체를 바꿀 수 있습니다.  
  
> [!NOTE]  
>  테이블에 파티션이 여러 개 있는 경우 테이블 속성 편집 대화 상자를 사용하여 행 필터 매핑을 변경할 수 없습니다. 파티션이 여러 개 있는 테이블에 대한 행 필터 매핑을 변경하려면 파티션 관리자를 사용합니다. 자세한 내용은 참조 [파티션을](../../analysis-services/tabular-models/partitions-ssas-tabular.md)합니다.  
  
#### <a name="to-change-table-column-or-row-filter-mappings"></a>테이블, 열 또는 행 필터 매핑을 변경하려면  
  
1.  모델 디자이너에서 테이블을 클릭한 다음 **테이블** 메뉴와 **테이블 속성**을 차례로 클릭합니다.  
  
2.  **테이블 속성 편집** 대화 상자에서 필터링할 조건이 포함된 열을 찾은 다음 열 머리글 오른쪽의 아래쪽 화살표를 클릭합니다.  
  
3.  **자동 필터** 메뉴에서 다음 중 하나를 수행합니다.  
  
    -   열 값 목록에서 필터링 기준으로 사용할 값을 하나 이상 선택하거나 취소한 다음 확인을 클릭합니다.  
  
         값의 수가 너무 많은 경우 개별 항목이 목록에 표시되지 않을 수 있습니다. 대신 "표시할 항목이 너무 많음"이라는 메시지가 나타납니다.  
  
    -   열 형식에 따라 **숫자 필터** 또는 **텍스트 필터** 를 클릭한 다음 같음과 같은 비교 연산자 명령 중 하나를 클릭하거나 사용자 지정 필터를 클릭합니다. **사용자 지정 필터** 대화 상자에서 필터를 만든 다음 **확인**을 클릭합니다.  
  
         실수가 있어 새로 시작해야 하는 경우 **행 필터 지우기**를 클릭하십시오.  
  
  
  
