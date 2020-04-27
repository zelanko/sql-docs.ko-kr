---
title: 데이터 세트 속성 대화 상자, 옵션(보고서 작성기) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10020"
ms.assetid: 43e50133-45ef-47a2-b575-34dfcc28ec98
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b174f9ad33ee38c2f47ffc8a684cddd7ea4376bf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107358"
---
# <a name="dataset-properties-dialog-box-options-report-builder"></a>데이터 세트 속성 대화 상자, 옵션(보고서 작성기)
  **데이터 세트 속성** 대화 상자에서 **옵션**을 선택하여 데이터 정렬 옵션 및 부분을 세부 데이터로 처리하는 옵션 등 쿼리에 대한 데이터 옵션을 변경할 수 있습니다. 데이터 정렬에 대한 자세한 내용은 [SQL Server 온라인 설명서](../../relational-databases/collations/collation-and-unicode-support.md) 에서 [데이터 정렬 및 유니코드 지원](https://go.microsoft.com/fwlink/?linkid=98335)을 참조하세요.  
  
 보고서 서버에 있는 공유 데이터 세트 정의의 일부인 데이터 옵션은 공유 데이터 세트를 사용하는 모든 보고서에 영향을 미칩니다. 공유 데이터 세트가 보고서에 추가된 후 해당 데이터 세트에 대한 옵션을 재정의할 수 있습니다. 이러한 변경 내용은 해당 옵션이 정의된 보고서에만 영향을 미칩니다.  
  
 포함된 데이터 세트에 대한 데이터 옵션은 해당 옵션이 정의된 보고서에만 영향을 미칩니다.  
  
 자세한 내용은 [보고서 포함된 데이터 세트 및 공유 데이터 세트&#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **데이터 정렬**  
 데이터 정렬에 사용할 데이터 정렬 시퀀스를 결정하는 로캘을 선택합니다. **Default** 로 설정하면 보고서가 실행될 때 보고서 서버가 데이터 공급자로부터 값을 가져와야 합니다. 값을 가져올 수 없는 경우 기본값이 컴퓨터의 로캘 설정에서 파생됩니다.  
  
 **대/소문자 구분**  
 대/소문자 구분을 결정하는 값을 선택합니다. 이 옵션은 데이터가 대/소문자를 구분하는지 여부를 나타냅니다. **대/소문자 구분** 은 **True**, **False**또는 **Auto**로 설정할 수 있습니다. 기본값인 **Auto**로 설정하면 보고서가 실행될 때 보고서 서버가 데이터 공급자로부터 값을 가져와야 합니다. 데이터 공급자가 대/소문자 구분 형식을 지원하지 않는 경우에는 이 값이 **False**인 것처럼 보고서가 실행됩니다. 지원되는 값을 알고 있는 경우 **True**를 선택합니다.  
  
 **악센트 구분**  
 악센트 구분을 결정하는 값을 선택합니다. **악센트 구분** 은 데이터가 악센트를 구분하는지 여부를 나타내며 **True**, **False**또는 **Auto**로 설정할 수 있습니다. 기본값인 **Auto**로 설정하면 보고서가 실행될 때 보고서 서버가 데이터 공급자로부터 값을 가져와야 합니다. 데이터 공급자가 악센트 구분 형식을 지원하지 않는 경우에는 이 값이 **False**인 것처럼 보고서가 실행됩니다. 지원되는 값을 알고 있는 경우 **True**를 선택합니다.  
  
 **일본어 가나 구분**  
 일본어 가나 구분을 결정하는 값을 선택합니다. 이 옵션은 데이터가 일본어 가나를 구분하는지 여부를 나타내며 **True**, **False**또는 **Auto**로 설정할 수 있습니다. 기본값인 **Auto**로 설정하면 보고서가 실행될 때 보고서 서버가 데이터 공급자로부터 값을 가져와야 합니다. 데이터 공급자가 일본어 가나 구분 형식을 지원하지 않는 경우에는 이 값이 **False**인 것처럼 보고서가 실행됩니다. 지원되는 값을 알고 있는 경우 **True**를 선택합니다.  
  
 **전자/반자 구분**  
 전자/반자 구분을 결정하는 값을 선택합니다. 이 옵션은 데이터가 전자/반자를 구분하는지 여부를 나타내며 **True**, **False**또는 **Auto**로 설정할 수 있습니다. 기본값인 **Auto**로 설정하면 보고서가 실행될 때 보고서 서버가 데이터 공급자로부터 값을 가져와야 합니다. 데이터 공급자가 전자/반자 구분 형식을 지원하지 않는 경우에는 이 값이 **False**인 것처럼 보고서가 실행됩니다. 지원되는 값을 알고 있는 경우 **True**를 선택합니다.  
  
 **부분합을 정보 행으로 해석**  
 부분합 행을 집계 행이 아니라 정보 행으로 해석할지 여부를 나타내는 값을 선택합니다. 기본값인 **Auto**는 보고서에서 () 함수를 `Aggregate`사용 하 여 데이터 집합의 필드에 액세스 하지 않는 경우 부분합 행이 정보 행으로 처리 되어야 함을 나타냅니다. 부분합 행을 집계 행으로 해석하려면 **False**를 선택합니다. 부분합 행을 정보 행으로 해석 하 고 `Aggregate`() 함수를 사용 하지 않도록 하려면 **True**를 선택 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [대화 상자, 창 및 마법사에 대 한 보고서 작성기 도움말](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [집계 함수 &#40;보고서 작성기 및 SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md)   
 [데이터 필터링, 그룹화 및 정렬 &#40;보고서 작성기 및 SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [보고서 포함 된 데이터 집합 및 공유 데이터 집합 &#40;보고서 작성기 및 SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [데이터 세트 속성 대화 상자, 쿼리&#40;보고서 작성기&#41;](dataset-properties-dialog-box-query-report-builder.md)  
  
  
