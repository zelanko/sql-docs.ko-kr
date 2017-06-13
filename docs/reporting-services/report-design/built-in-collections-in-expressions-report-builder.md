---
title: "식 (보고서 작성기 및 SSRS)의 기본 제공 컬렉션 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 78d5e3b8-9320-4e4b-a025-e2de3cf7afa7
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ff834d00c915ae81179ff9b0bebed19e7c9ec6c1
ms.contentlocale: ko-kr
ms.lasthandoff: 06/13/2017

---
# <a name="built-in-collections-in-expressions-report-builder"></a>식 (보고서 작성기)에서 기본 제공 컬렉션
  보고서의 식에는 ReportItems, 매개 변수, 필드, 데이터 집합, 데이터 원본, 변수 및 보고서 이름과 같은 전역 정보에 대한 기본 제공 필드 등 기본 제공 컬렉션에 대한 참조가 포함될 수 있습니다. **식** 대화 상자에 표시되지 않는 컬렉션도 있습니다. DataSets 및 DataSources 컬렉션은 보고서 서버의 게시된 보고서에 대해 런타임에만 사용할 수 있습니다. ReportItems 컬렉션은 페이지 또는 페이지 머리글의 입력란과 같이 보고서 영역에 있는 입력란의 컬렉션입니다.  
  
 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Collections"></a> 기본 제공 컬렉션 이해  
 다음 표에서는 식을 작성할 때 사용할 수 있는 기본 제공 컬렉션을 보여 줍니다. 각 행에는 컬렉션에 대한 대/소문자 구분 프로그래밍 이름, 식 대화 상자를 사용하여 컬렉션에 대한 참조를 대화형으로 추가할 수 있는지 여부, 예, 그리고 컬렉션 값이 초기화되어 사용 가능해지는 시점을 포함한 설명이 포함됩니다.  
  
|기본 제공 컬렉션|식 대화 상자의 범주|예제|Description|  
|--------------------------|-------------------------------------------|-------------|-----------------|  
|**Globals**|기본 제공 필드|`=Globals.ReportName`<br /><br /> `- or -`<br /><br /> `=Globals.PageNumber`|보고서 이름이나 페이지 번호를 비롯하여 보고서에 유용한 전역 변수를 나타냅니다. 항상 사용할 수 있습니다.<br /><br /> 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.|  
|**사용자**|기본 제공 필드|`=User.UserID`<br /><br /> -또는-<br /><br /> `=User.Language`|언어 설정 또는 사용자 ID를 비롯하여 보고서를 실행하는 사용자에 대한 데이터 컬렉션을 나타냅니다. 항상 사용할 수 있습니다.<br /><br /> 자세한 내용은 [기본 제공 Globals 및 Users 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)를 참조하세요.|  
|**매개 변수**|매개 변수|`=Parameters("ReportMonth").Value`<br /><br /> -또는-<br /><br /> `=Parameters!ReportYear.Value`|각각 단일 값 또는 다중값일 수 있는 보고서 매개 변수 컬렉션을 나타냅니다. 초기화 처리가 완료된 다음에만 사용할 수 있습니다. 자세한 내용은 [매개 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)를 참조하세요.|  
|**Fields(** *\<Dataset>* **)**|필드|`=Fields!Sales.Value`|보고서에 사용할 수 있는 데이터 집합의 필드 컬렉션을 나타냅니다. 데이터 원본에 있는 데이터를 검색하여 데이터 집합으로 가져온 다음 사용할 수 있습니다. 자세한 내용은 [데이터 집합 필드 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)를 참조하세요.|  
|**DataSets**|표시되지 않음|`=DataSets("TopEmployees").CommandText`|보고서 정의 본문에서 참조하는 데이터 집합 컬렉션을 나타냅니다. 페이지 머리글이나 페이지 바닥글에만 사용되는 데이터 원본은 포함되지 않습니다. 로컬 미리 보기에서는 사용할 수 없습니다. 자세한 내용은 [DataSources 및 DataSets 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md)를 참조하세요.|  
|**DataSources**|표시되지 않음|`=DataSources("AdventureWorks2012").Type`|보고서 본문에서 참조하는 데이터 원본 컬렉션을 나타냅니다. 페이지 머리글이나 페이지 바닥글에만 사용되는 데이터 원본은 포함되지 않습니다. 로컬 미리 보기에서는 사용할 수 없습니다. 자세한 내용은 [DataSources 및 DataSets 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-datasources-and-datasets-references-report-builder.md)를 참조하세요.|  
|**변수**|`Variables`|`=Variables!CustomTimeStamp.Value`|보고서 변수 및 그룹 변수의 컬렉션을 나타냅니다. 자세한 내용은 [보고서 및 그룹 변수 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-report-and-group-variables-references-report-builder.md)를 참조하세요.|  
|**ReportItems**|표시되지 않음|`=ReportItems("Textbox1").Value`|보고서 항목에 대한 입력란의 컬렉션을 나타냅니다. 이 컬렉션은 페이지 머리글 또는 페이지 바닥글에 포함할 페이지 항목을 요약하는 데 사용할 수 있습니다. 자세한 내용은 [ReportItems 컬렉션 참조&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/built-in-collections-reportitems-collection-references-report-builder.md)를 참조하세요.|  
  
##  <a name="Syntax"></a> 식에서 컬렉션 구문 사용  
 식에서 컬렉션을 참조하려면 컬렉션의 항목에 대한 표준 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 구문을 사용합니다. 다음 표에서는 컬렉션 구문의 예를 보여 줍니다.  
  
|구문|예제|  
|------------|-------------|  
|*Collection!ObjectName.Property*|`=Fields!Sales.Value`|  
|*Collection!ObjectName("Property")*|`=Fields!Sales("Value")`|  
|*Collection("ObjectName").Property*|`=Fields("Sales").Value`|  
|*Collection("Member")*|`=User("Language")`|  
|*Collection.Member*|`=User.Language`|  
  
## <a name="see-also"></a>관련 항목:  
 [식 추가&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)   
 [식 예&#40;보고서 작성기 및 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
