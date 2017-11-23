---
title: "Column 요소 (DTA) 인덱스에 대 한 | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 557befbb53d96bd0d1b5f862b6df5eeb63670b17
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="column-element-for-index-dta"></a>Index의 Column 요소(DTA)
  사용자 지정 구성에서 인덱스가 만들어지는 열을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
 **Type**: 선택 사항입니다. 인덱스 열 유형을 지정합니다. **string** 데이터 형식을 사용하여 허용된 다음 값 중 하나로 이 특성을 지정할 수 있습니다.  
  
-   **KeyColumn**  
  
     인덱스 키에서 열을 참조하도록 지정합니다. 다음 구문을 사용하여 이 특성을 설정합니다.  
  
    ```  
    <Column Type="KeyColumn">  
    ```  
  
     자세한 내용은 [클러스터형 및 비클러스터형 인덱스 소개](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)를 참조하세요.  
  
-   **IncludedColumn**  
  
     열이 키 열 대신에 포괄 열이라는 것을 지정합니다. 다음 구문을 사용하여 이 특성을 설정합니다.  
  
    ```  
    <Column Type="IncludedColumn">  
    ```  
  
     키가 아닌 열 포함에 대한 자세한 내용은 [포괄 열을 사용하여 인덱스 만들기](../../relational-databases/indexes/create-indexes-with-included-columns.md)를 참조하세요.  
  
 **SortOrder**: 선택 사항입니다. 열의 정렬 순서를 지정합니다. 다음과 같이 **string** 데이터 형식을 사용하여 **"Ascending"** 또는 **"Descending"** 정렬 순서를 지정할 수 있습니다.  
  
```  
<Column SortOrder="Ascending">  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**Index** 요소에 최대 1024개의 열을 지정할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Index 요소&#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**자식 요소**|[Column의 Name 요소&#40;DTA&#41;](../../tools/dta/name-element-for-column-dta.md)|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
