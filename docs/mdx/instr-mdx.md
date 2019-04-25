---
title: Instr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f4bfab3bc18958a51bb05c68e90c17a1359d046
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629093"
---
# <a name="instr-mdx"></a>Instr (MDX)


  다른 문자열 내에서 한 문자열의 시작 위치를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
InStr([start, ]searched_string, search_string[, compare])  
```  
  
## <a name="arguments"></a>인수  
 *start*  
 (선택 사항) 각 검색의 시작 위치를 설정하는 숫자 식입니다. 이 값을 생략하면 첫 번째 문자 위치에서 검색이 시작됩니다. start가 null인 경우에는 함수 반환 값이 정의되지 않습니다.  
  
 *searched_string*  
 검색할 문자열 식입니다.  
  
 *search_string*  
 검색할 문자열 식입니다.  
  
 *Compare*  
 (선택 사항) 정수 값입니다. 이 인수는 항상 무시되며, 다른 호환성을 위해 정의 된 **Instr** 다른 언어의 함수입니다.  
  
## <a name="return-value"></a>반환 값  
 시작 위치를 사용 하 여 정수 값 *String2* 에 *String1*합니다.  
  
 또한 **InStr** 함수는 조건에 따라 다음 표의 값을 반환 합니다.  
  
|조건|반환 값|  
|---------------|------------------|  
|String1의 길이가 0인 경우|영 (0)|  
|String1이 Null인 경우|정의되지 않음|  
|String2의 길이가 0인 경우|start|  
|String2가 Null인 경우|정의되지 않음|  
|String2를 찾을 수 없는 경우|영 (0)|  
|start가 Len(String2)보다 큰 경우|영 (0)|  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]  
>  **Instr** 항상 대/소문자 구분 비교를 수행 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 합니다 **Instr** 함수와 다른 표시 될 시나리오입니다.  
  
```  
with   
    member [Date].[Date].[Results] as "Results"  
    member measures.[lowercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[uppercase found in lowercase string] as InStr( "abcdefghijklmnñopqrstuvwxyz", "O")  
    member measures.[searched string is empty]            as InStr( "", "o")  
    member measures.[searched string is null]             as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[search string is empty]              as InStr( "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is empty start 10]     as InStr(10, "abcdefghijklmnñopqrstuvwxyz", "")  
    member measures.[search string is null]               as iif(IsError(InStr( null, "o")), "Is Error", iif(IsNull(InStr( null, "o")), "Is Null","Is undefined"))  
    member measures.[found from start 10]                 as InStr( 10, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NOT found from start 17]             as InStr( 17, "abcdefghijklmnñopqrstuvwxyz", "o")  
    member measures.[NULL start]                          as iif(IsError(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Error", iif(IsNull(InStr( null, "abcdefghijklmnñopqrstuvwxyz", "o")), "Is Null","Is undefined"))  
    member measures.[start greater than searched length]  as InStr( 170, "abcdefghijklmnñopqrstuvwxyz", "o")  
  
select  [Results] on columns,  
       { measures.[lowercase found in lowercase string]  
       , measures.[uppercase found in lowercase string]  
       , measures.[searched string is empty]  
       , measures.[searched string is null]  
       , measures.[search string is empty]  
       , measures.[search string is empty start 10]  
       , measures.[search string is null]  
       , measures.[found from start 10]  
       , measures.[NOT found from start 17]  
       , measures.[NULL start]   
       , measures.[start greater than searched length]  
       } on rows  
  
from [Adventure Works]  
```  
  
 다음 표에서는 얻게 되는 결과를 보여 줍니다.  
  
|||  
|-|-|  
||결과|  
|소문자 문자열에 소문자가 있습니다.|16|  
|소문자 문자열에 대문자가 있습니다.|16|  
|검색된 문자열이 비어 있습니다.|0|  
|검색된 문자열이 null입니다.|정의되지 않음|  
|검색 문자열이 비어 있습니다.|1|  
|검색 문자열이 비어 있습니다(start 10).|10|  
|검색 문자열이 null입니다.|정의되지 않음|  
|start 10에서 찾았습니다.|16|  
|start 17에서 찾을 수 없습니다.|0|  
|NULL start|정의되지 않음|  
|start가 검색된 길이보다 큽니다.|0|  
  
  
