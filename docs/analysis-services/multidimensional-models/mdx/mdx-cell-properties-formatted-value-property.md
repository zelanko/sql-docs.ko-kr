---
title: "LANGUAGE 및 FORMAT_STRING FORMATTED_VALUE에서 | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 465b5ce3730dc73357502ff88517eb3c5dd29d20
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-properties---formattedvalue-property"></a>MDX 셀 속성-FORMATTED_VALUE 속성
  FORMATTED_VALUE 속성은 셀의 VALUE, FORMAT_STRING 속성 및 LANGUAGE 속성의 상호 작용을 기반으로 합니다. 이 항목에서는 이러한 속성이 상호 작용하여 FORMATTED_VALUE 속성을 작성하는 방법에 대해 설명합니다.  
  
## <a name="value-formatstring-language-properties"></a>VALUE, FORMAT_STRING, LANGUAGE 속성  
 다음 표에서는 이러한 속성에 대해 설명합니다. 사용자는 이 내용을 통해 이러한 속성을 조합하여 사용하는 방법을 알 수 있습니다.  
  
 VALUE  
 형식이 지정되지 않은 셀 값입니다.  
  
 FORMAT_STRING  
 FORMATTED_VALUE 속성을 생성하기 위해 셀 값에 적용될 형식 지정 템플릿입니다.  
  
 LANGUAGE  
 FORMATTED_VALUE의 지역화된 버전을 생성하기 위해 FORMAT_STRING과 함께 적용될 로캘 사양입니다.  
  
## <a name="formattedvalue-constructed"></a>FORMATTED_VALUE 생성  
 VALUE 속성 값을 사용하고 해당 값에 FORMAT_STRING 속성에 지정된 형식 템플릿을 적용하여 FORMATTED_VALUE 속성을 생성합니다. 또한 형식 지정 값이 **명명된 형식 지정 리터럴** 인 경우 LANGUAGE 속성 사양이 명명된 형식 지정에 대한 언어 사용법에 따라 FORMAT_STRING의 출력을 수정합니다. 명명된 형식 지정 리터럴은 모두 지역화할 수 있는 방법으로 정의됩니다. 예를 들어 `"General Date"` 는 언어 사양에 상관없이 템플릿에서 정의하는 대로 날짜를 표시해야 함을 지정하는 `"YYYY-MM-DD hh:nn:ss",` 템플릿과는 반대로 지역화할 수 있는 사양입니다.  
  
 FORMAT_STRING 템플릿과 LANGUAGE 사양 사이에 충돌이 있으면 FORMAT_STRING 템플릿이 LANGUAGE 사양보다 우선 적용됩니다. 예를 들어 FORMAT_STRING="$ #0" 및 LANGUAGE=1034(스페인), VALUE=123.456인데 FORMATTED_VALUE="  123" 대신 FORMATTED_VALUE="$ 123"인 경우 형식 템플릿의 값이 지정된 언어보다 우선 적용되므로 예상 형식은 유로입니다.  
  
### <a name="examples"></a>예  
 다음 예에서는 LANGUAGE가 FORMAT_STRING과 함께 사용될 때 얻은 출력을 보여 줍니다.  
  
 첫 번째 예에서는 숫자 값 형식 지정에 대해 설명하고 두 번째 예에서는 날짜 및 시간 값 형식 지정에 대해 설명합니다.  
  
 각 예에서 MDX(Multidimensional Expressions) 코드가 제공됩니다.  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 위의 MDX 쿼리를 로캘 1033가 있는 서버 및 클라이언트에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 실행한 경우 바뀐 결과는 다음과 같습니다.  
  
|멤버|FORMATTED_VALUE|설명|  
|------------|----------------------|-----------------|  
|변수를 잠그기 위한|$5,040.00|FORMAT_STRING이 `Currency` 로 설정되었고 LANGUAGE가 `1033`(시스템 로캘 값에서 상속)입니다.|  
|B|5.040,00|FORMAT_STRING이 `Currency` (A에서 상속)로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인)로 설정되었으므로 유로 기호, 다른 소수 구분 기호 및 다른 천 단위 구분 기호가 표시됩니다.|  
|C|$5.040,00|FORMAT_STRING이 `$#,##0.00` (A에서 상속된 Currency에 대한 재정의)으로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인)로 설정되었습니다. FORMAT_STRING 속성이 명시적으로 통화 기호를 $로 설정했으므로 FORMATTED_VALUE가 $ 기호와 함께 표시됩니다. 그러나 `.` (점) 및 `,` (쉼표)가 각각 소수 구분 기호와 천 단위 구분 기호의 자리 표시자이므로 언어 사양은 소수 구분 기호와 천 단위 구분 기호에 대해 지역화된 출력을 생성하면서 이러한 기호에 영향을 줍니다.|  
|D|5.04E+03|FORMAT_STRING이 `Scientific` 로 설정되었고 LANGUAGE가 `1033`(시스템 로캘 값에서 상속)으로 설정되었으므로 `.` (점)이 소수 구분 기호입니다.|  
|E|5,04E+03|FORMAT_STRING이 `Scientific` 으로 설정되었고 LANGUAGE가 명시적으로 `1034,` 로 설정되었으므로 `,` (쉼표)가 소수 구분 기호입니다.|  
|F|50.40%|FORMAT_STRING이 `Percent` 로 설정되었고 LANGUAGE가 `1033`(시스템 로캘 값에서 상속)으로 설정되었으므로 `.` (점)이 소수 구분 기호입니다.<br /><br /> VALUE가 5040에서 0.5040으로 변경되었습니다.|  
|G|50,40%|FORMAT_STRING이 `Percent`(F에서 상속)로 설정되었고 LANGUAGE가 명시적으로 `1034` 로 설정되었으므로 `,` (쉼표)가 소수 구분 기호입니다.<br /><br /> VALUE가 F 값에서 상속되었습니다.|  
|H|아니오|FORMAT_STRING이 `YES/NO`로 설정되었고 VALUE가 0으로 설정되었고 LANGUAGE가 명시적으로 `1034`로 설정되었습니다. 영어 NO와 스페인어 NO 사이의 차이가 없으므로 사용자는 FORMATTED_VALUE의 차이점을 발견할 수 없습니다.|  
|I|SI|FORMAT_STRING이 `YES/NO`로 설정되었고 VALUE가 59로 설정되었고 LANGUAGE가 명시적으로 `1034`로 설정되었습니다. YES/NO 형식 지정에 대해 정의된 대로 0과 다른 값은 YES이고 언어가 스페인어로 설정되었으므로 FORMATTED_VALUE가 SI입니다.|  
|J|Desactivado|FORMAT_STRING이 `ON/OFF`로 설정되었고 VALUE가 0으로 설정되었고 LANGUAGE가 명시적으로 `1034`로 설정되었습니다. ON/OFF 형식 지정에 대해 정의된 대로 0과 같은 값은 OFF이고 언어가 스페인어로 설정되었으므로 FORMATTED_VALUE가 Desactivado입니다.|  
|K|Activado|FORMAT_STRING이 `ON/OFF`로 설정되었고 VALUE가 -312로 설정되었고 LANGUAGE가 명시적으로 `1034`로 설정되었습니다. ON/OFF 형식 지정에 대해 정의된 대로 0과 다른 값은 ON이고 언어가 스페인어로 설정되었으므로 FORMATTED_VALUE가 Activado입니다.|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 위의 MDX 쿼리를 로캘 1033가 있는 서버 및 클라이언트에서 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 실행한 경우 바뀐 결과는 다음과 같습니다.  
  
|멤버|FORMATTED_VALUE|설명|  
|------------|----------------------|-----------------|  
|변수를 잠그기 위한|3/12/1959 6:30:00 AM|FORMAT_STRING이 CDate() 식에 의해 암시적으로 `General Date` 로 설정되었고 LANGUAGE가 `1033` (영어)(시스템 로캘 값에서 상속)으로 설정되었습니다.|  
|B|Thursday, March 12, 1959|FORMAT_STRING이 명시적으로 `Long Date` 로 설정되었고 LANGUAGE가 `1033` (영어)(시스템 로캘 값에서 상속)입니다.|  
|C|12/03/1959 6:30:00|FORMAT_STRING이 명시적으로 `General Date` 로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인어)입니다.<br /><br /> 미국 형식 지정 스타일과 비교해 보면 월과 일이 바뀌었습니다.|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING이 명시적으로 `Long Date` 로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인어)입니다.<br /><br /> 월과 요일은 스페인어로 표시됩니다.|  
|E|1959/03/12 6:30:00|FORMAT_STRING이 명시적으로 `General Date` 로 설정되었고 LANGUAGE가 명시적으로 `1041` (일본어)입니다.<br /><br /> 이제 날짜의 형식이 연도/월/일 시간:분:초입니다.|  
|F|1959年3月12日|FORMAT_STRING이 명시적으로 `Long Date` 로 설정되었고 LANGUAGE가 명시적으로 `1041` (일본어)입니다.|  
|G|오전 6:30:00|FORMAT_STRING이 명시적으로 `Long Time` 으로 설정되었고 LANGUAGE가 `1033` (영어)(시스템 로캘 값에서 상속)입니다.|  
|H|06:30|FORMAT_STRING이 명시적으로 `Short Time` 으로 설정되었고 LANGUAGE가 `1033` (영어)(시스템 로캘 값에서 상속)입니다.|  
|I|6:30:00|FORMAT_STRING이 명시적으로 `Long Time` 으로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인어)로 설정되었습니다.|  
|J|06:30|FORMAT_STRING이 명시적으로 `Short Time` 으로 설정되었고 LANGUAGE가 명시적으로 `1034` (스페인어)로 설정되었습니다.|  
|K|6:30:00|FORMAT_STRING이 명시적으로 `Long Time` 으로 설정되었고 LANGUAGE가 명시적으로 `1041` (일본어)로 설정되었습니다.|  
|L|06:30|FORMAT_STRING이 명시적으로 `Short Time` 으로 설정되었고 LANGUAGE가 명시적으로 `1041` (일본어)로 설정되었습니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [FORMAT_STRING 내용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [셀 속성 &#40;를 사용 하 여 Mdx&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [만들기 및 속성 값 &#40; 사용 Mdx&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [MDX 쿼리 기본 사항&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

