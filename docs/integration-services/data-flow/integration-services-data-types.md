---
title: Integration Services 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
caps.latest.revision: 98
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fce885002fc8dd2870480327ed575b77332ed0d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="integration-services-data-types"></a>Integration Services 데이터 형식
  데이터가 패키지의 데이터 흐름으로 들어갈 때 데이터를 추출하는 원본은 데이터를 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식으로 변환합니다. 숫자 데이터에는 숫자 데이터 형식이 지정되고, 문자열 데이터에는 문자 데이터 형식이, 그리고 날짜에는 날짜 데이터 형식이 지정됩니다. 또한 GUID 및 BLOB(Binary Large Object Block)과 같은 다른 데이터에는 해당 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식이 지정됩니다. 데이터에 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식과 호환되지 않는 데이터 형식이 있는 경우에는 오류가 발생합니다.  
  
 일부 데이터 흐름 구성 요소는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식과 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 관리 데이터 형식 간의 데이터 형식을 변환합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 와 관리 데이터 형식 간 매핑에 대한 자세한 내용은 [데이터 흐름의 데이터 형식 작업](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)을 참조하세요.  
  
 다음 표에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식을 나열합니다. 이 표의 일부 데이터 형식에는 해당 형식에 적용되는 전체 자릿수 및 소수 자릿수 정보가 있습니다. 전체 자릿수 및 소수 자릿수에 대한 자세한 내용은 [전체 자릿수, 소수 자릿수 및 길이&#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)를 참조하세요.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|DT_BOOL|부울 값입니다.|  
|DT_BYTES|이진 데이터 값입니다. 길이는 가변적이고 최대 길이는 8000바이트입니다.|  
|DT_CY|통화 값입니다. 이 데이터 형식은 부호 있는 8바이트 정수이며 소수 자릿수는 4이고 최대 전체 자릿수는 19자리입니다.|  
|DT_DATE|연도, 월, 일, 시간, 분, 초 및 소수 자릿수 초로 구성된 날짜 구조입니다.  소수 자릿수 초의 자릿수는 7자리로 고정되어 있습니다.<br /><br /> DT_DATE 데이터 형식은 8바이트 부동 소수점 수를 사용하여 구현됩니다. 일은 정수 증분으로 표시되며 1899년 12월 30일부터 시작하여 자정을 0시로 표시합니다. 시간 값은 숫자에서 소수 부분의 절대값으로 표시됩니다. 그러나 부동 소수점 값은 실수 값을 모두 나타낼 수 없으므로 DT_DATE로 나타낼 수 있는 날짜 범위는 제한되어 있습니다.<br /><br /> 반면 DT_DBTIMESTAMP는 내부적으로 연도, 월, 일, 시간, 분, 초 및 밀리초에 대한 개별 필드가 있는 구조로 표시됩니다. 이 데이터 형식은 나타낼 수 있는 날짜 범위 제한이 보다 넓습니다.|  
|DT_DBDATE|연도, 월 및 일로 구성된 날짜 구조입니다.|  
|DT_DBTIME|시간, 분 및 초로 구성된 시간 구조입니다.|  
|DT_DBTIME2|시간, 분, 초 및 소수 자릿수 초로 구성된 시간 구조입니다. 소수 자릿수 초의 최대 자릿수는 7자리입니다.|  
|DT_DBTIMESTAMP|연도, 월, 일, 시간, 분, 초 및 소수 자릿수 초로 구성된 타임스탬프 구조입니다. 소수 자릿수 초의 최대 자릿수는 3자리입니다.|  
|DT_DBTIMESTAMP2|연도, 월, 일, 시간, 분, 초 및 소수 자릿수 초로 구성된 타임스탬프 구조입니다. 소수 자릿수 초의 최대 자릿수는 7자리입니다.|  
|DT_DBTIMESTAMPOFFSET|연도, 월, 일, 시간, 분, 초 및 소수 자릿수 초로 구성된 타임스탬프 구조입니다. 소수 자릿수 초의 최대 자릿수는 7자리입니다.<br /><br /> DT_DBTIMESTAMP 및 DT_DBTIMESTAMP2 데이터 형식과 달리 DT_DBTIMESTAMPOFFSET 데이터 형식에는 표준 시간대 오프셋이 있습니다. 이 오프셋은 시간이 UTC(Coordinated Universal Time)에서 오프셋되는 시간과 분을 지정합니다. 표준 시간대 오프셋은 시스템에서 현지 시간을 가져오는 데 사용됩니다.<br /><br /> 표준 시간대 오프셋에는 UTC에서 오프셋을 더했는지, 아니면 뺐는지를 나타내기 위해 + 또는 - 기호를 포함해야 합니다. 시간 오프셋의 유효한 숫자는 -14에서 +14 사이입니다. 분 오프셋의 기호는 다음과 같이 시간 오프셋의 기호에 따라 달라집니다.<br /><br /> 시간 오프셋의 기호가 음수이면 분 오프셋이 음수이거나 0이어야 합니다.<br /><br /> 시간 오프셋의 기호가 양수이면 분 오프셋이 양수이거나 0이어야 합니다.<br /><br /> 시간 오프셋의 기호가 0이면 분 오프셋이 -0.59에서 +0.59 사이의 값이 될 수 있습니다.|  
|DT_DECIMAL|전체 자릿수 및 소수 자릿수가 고정된 정확한 숫자 값입니다. 이 데이터 형식은 별개의 부호가 포함된 12바이트의 부호 없는 정수이며 소수 자릿수는 0에서 28이고 최대 전체 자릿수는 29입니다.|  
|DT_FILETIME|1601년 1월 1일부터 100나노초 간격의 수를 나타내는 64비트 값입니다. 소수 자릿수 초의 최대 자릿수는 3자리입니다.|  
|DT_GUID|GUID(Globally Unique Identifier)입니다.|  
|DT_I1|1바이트의 부호 있는 정수입니다.|  
|DT_I2|2바이트의 부호 있는 정수입니다.|  
|DT_I4|4바이트의 부호 있는 정수입니다.|  
|DT_I8|8바이트의 부호 있는 정수입니다.|  
|DT_NUMERIC|전체 자릿수 및 소수 자릿수가 고정된 정확한 숫자 값입니다. 이 데이터 형식은 별개의 부호가 포함된 16바이트의 부호 없는 정수이며 소수 자릿수는 0에서 38이고 최대 전체 자릿수는 38입니다.|  
|DT_R4|단정밀도의 부동 소수점 값입니다.|  
|DT_R8|배정밀도의 부동 소수점 값입니다.|  
|DT_STR|최대 길이가 8000자인 Null 종료 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 문자열입니다. 열 값에 추가 Null 종결자가 들어 있으면 해당 문자열은 첫 번째 Null이 나타나는 위치에서 잘립니다.|  
|DT_UI1|1바이트의 부호 없는 정수입니다.|  
|DT_UI2|2바이트의 부호 없는 정수입니다.|  
|DT_UI4|4바이트의 부호 없는 정수입니다.|  
|DT_UI8|8바이트의 부호 없는 정수입니다.|  
|DT_WSTR|최대 길이가 4000자인 Null 종료 유니코드 문자열입니다. 열 값에 추가 Null 종결자가 들어 있으면 해당 문자열은 첫 번째 Null이 나타나는 위치에서 잘립니다.|  
|DT_IMAGE|최대 크기가 2^31-1(2,147,483,647)바이트인 이진 값입니다. 의 관리 데이터 형식 간의 데이터 형식을 변환합니다.|  
|DT_NTEXT|최대 길이가 2^30-1(1,073,741,823)자인 유니코드 문자열입니다.|  
|DT_TEXT|최대 길이가 2^31-1(2,147,483,647)자인 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 문자열입니다.|  
  
## <a name="conversion-of-data-types"></a>데이터 형식 변환  
 열의 데이터에 원본 데이터 형식으로 할당된 전체 너비가 필요하지 않은 경우 열의 데이터 형식을 변경할 수 있습니다. 각 행이 좁을수록 원본에서 대상으로 데이터를 이동하는 속도가 빨라지기 때문에 각 데이터 행을 가능한 한 좁게 만들면 데이터 전송 시 성능을 최적화할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 숫자 데이터 형식이 모두 포함되어 있으므로 데이터의 크기와 적합한 데이터 형식을 찾아 볼 수 있습니다. 예를 들어 데이터 형식이 DT_UI8인 열의 값이 항상 0에서 3000 사이의 정수인 경우 데이터 형식을 DT_UI2로 변경할 수 있습니다. 마찬가지로, 데이터 형식이 DT_CY인 열에 대해 정수 데이터 형식을 대신 사용해도 패키지의 데이터 요구 사항에 문제가 없다면 해당 데이터 형식을 DT_I4로 변경할 수 있습니다.  
  
 열의 데이터 형식은 다음과 같은 방식으로 변경할 수 있습니다.  
  
-   식을 사용하여 데이터 형식을 암시적으로 변환합니다. 자세한 내용은 [식에서의 Integration Services 데이터 형식](../../integration-services/expressions/integration-services-data-types-in-expressions.md), [식에서의 Integration Services 데이터 형식](../../integration-services/expressions/integration-services-data-types-in-expressions.md) 및 [Integration Services&#40;SSIS&#41; 식](../../integration-services/expressions/integration-services-ssis-expressions.md)을 참조하세요.  
  
-   캐스트 연산자를 사용하여 데이터 형식을 변환합니다. 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
-   데이터 변환을 사용하여 열의 데이터 형식을 한 데이터 형식에서 다른 데이터 형식으로 캐스팅합니다. 자세한 내용은 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)을 참조하세요.  
  
-   파생 열 변환을 사용하여 원래 열과 데이터 형식이 다른 열의 복사본을 만듭니다. 자세한 내용은 [파생 열 변환](../../integration-services/data-flow/transformations/derived-column-transformation.md)을 참조하세요.  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>문자열과 날짜/시간 데이터 형식 간 변환  
 다음 표에서는 날짜/시간 데이터 형식과 문자열 간의 캐스팅 또는 변환 결과를 보여 줍니다.  
  
-   캐스트 연산자나 데이터 변환을 사용하는 경우 날짜 또는 시간 데이터 형식이 해당 문자열 형식으로 변환됩니다. 예를 들어 DT_DBTIME 데이터 형식은 "hh:mm:ss" 형식의 문자열로 변환됩니다.  
  
-   문자열을 날짜 또는 시간 데이터 형식으로 변환하려면 문자열에 원하는 날짜 또는 시간 데이터 형식에 해당하는 문자열 형식을 사용해야 합니다. 예를 들어 일부 날짜 문자열을 DT_DBDATE 데이터 형식으로 성공적으로 변환하려면 이러한 날짜 문자열이 "yyyy-mm-dd" 형식이어야 합니다.  
  
    |데이터 형식|문자열 형식|  
    |---------------|-------------------|  
    |DT_DBDATE|yyyy-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 DT_FILETIME 및 DT_DBTIMESTAMP의 형식에서 fff는 소수 자릿수 초를 나타내는 0에서 999 사이의 값입니다.  
  
 DT_DBTIMESTAMP2, DT_DBTIME2 및 DT_DBTIMESTAMPOFFSET의 날짜 형식에서 fffffff는 소수 자릿수 초를 나타내는 0에서 9999999 사이의 값입니다.  
  
 DT_DBTIMESTAMPOFFSET의 날짜 형식에는 표준 시간대 요소도 포함되어 있습니다. 시간 요소와 표준 시간대 요소 사이에는 공백이 있습니다.  
  
### <a name="converting-datetime-data-types"></a>날짜/시간 데이터 형식 변환  
 날짜/시간 데이터가 포함된 열의 데이터 형식을 변경하여 데이터의 날짜 또는 시간 부분을 추출할 수 있습니다. 다음 표에서는 한 날짜/시간 데이터 형식을 다른 날짜/시간 데이터 형식으로 변경한 결과를 나열합니다.  
  
#### <a name="converting-from-dtfiletime"></a>DT_FILETIME에서 변환  
  
|DT_FILETIME 변환 대상|결과|  
|-----------------------------|------------|  
|DT_FILETIME|변경되지 않습니다.|  
|DT_DATE|데이터 형식을 변환합니다.|  
|DT_DBDATE|시간 값을 제거합니다.|  
|DT_DBTIME|날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME 데이터 형식이 포함할 수 있는 소수 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIME2|DT_FILETIME 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP|데이터 형식을 변환합니다.|  
|DT_DBTIMESTAMP2|소수 자릿수가 DT_DBTIMESTAMP2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 표준 시간대 필드를 0으로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMPOFFSET 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
  
#### <a name="converting-from-dtdate"></a>DT_DATE에서 변환  
  
|DT_DATE 변환 대상|결과|  
|-------------------------|------------|  
|DT_FILETIME|데이터 형식을 변환합니다.|  
|DT_DATE|변경되지 않습니다.|  
|DT_DBDATE|DT_DATA 데이터 형식이 나타내는 시간 값을 제거합니다.|  
|DT_DBTIME|DT_DATE 데이터 형식이 나타내는 날짜 값을 제거합니다.|  
|DT_DBTIME2|DT_DATE 데이터 형식이 나타내는 날짜 값을 제거합니다.|  
|DT_DBTIMESTAMP|데이터 형식을 변환합니다.|  
|DT_DBTIMESTAMP2|데이터 형식을 변환합니다.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 표준 시간대 필드를 0으로 설정합니다.|  
  
#### <a name="converting-from-dtdbdate"></a>DT_DBDATE에서 변환  
  
|DT_DBDATE 변환 대상|결과|  
|---------------------------|------------|  
|DT_FILETIME|DT_FILETIME 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DATE|DT_DATE 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DBDATE|변경되지 않습니다.|  
|DT_DBTIME|DT_DBTIME 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DBTIME2|DT_DBTIME2 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP 데이터 형식의 시간 필드를 0으로 설정합니다.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 시간 필드와 표준 시간대 필드를 0으로 설정합니다.|  
  
#### <a name="converting-from-dtdbtime"></a>DT_DBTIME에서 변환  
  
|DT_DBTIME 변환 대상|결과|  
|---------------------------|------------|  
|DT_FILETIME|DT_FILETIME 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DATE|DT_DATE 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DBDATE|DT_DBDATE 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DBTIME|변경되지 않습니다.|  
|DT_DBTIME2|데이터 형식을 변환합니다.|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP2 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 날짜 필드와 표준 시간대 필드를 각각 현재 날짜와 0으로 설정합니다.|  
  
#### <a name="converting-from-dtdbtime2"></a>DT_DBTIME2에서 변환  
  
|DT_DBTIME2 변환 대상|결과|  
|----------------------------|------------|  
|DT_FILETIME|DT_FILETIME 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.<br /><br /> 소수 자릿수가 DT_FILETIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DATE|DT_DATE 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.<br /><br /> 소수 자릿수가 DT_DATE 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBDATE|DT_DBDATE 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.|  
|DT_DBTIME|소수 자릿수가 DT_DBTIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIME2|소수 자릿수가 대상 DT_DBTIME2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMP 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP2 데이터 형식의 날짜 필드를 현재 날짜로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMP2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 날짜 필드와 표준 시간대 필드를 각각 현재 날짜와 0으로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMPOFFSET 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
  
#### <a name="converting-from-dtdbtimestamp"></a>DT_DBTIMESTAMP에서 변환  
  
|DT_DBTIMESTAMP 변환 대상|결과|  
|--------------------------------|------------|  
|DT_FILETIME|데이터 형식을 변환합니다.|  
|DT_DATE|DT_DBTIMESTAMP 데이터 형식이 나타내는 값이 DT_DATE 데이터 형식의 범위를 오버플로하는 경우 DB_E_DATAOVERFLOW 오류를 반환합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBDATE|DT_DBTIMESTAMP 데이터 형식이 나타내는 시간 값을 제거합니다.|  
|DT_DBTIME|DT_DBTIMESTAMP 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIME2|DT_DBTIMESTAMP 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP|변경되지 않습니다.|  
|DT_DBTIMESTAMP2|소수 자릿수가 DT_DBTIMESTAMP2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 표준 시간대 필드를 0으로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMPOFFSET 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>DT_DBTIMESTAMP2에서 변환  
  
|DT_DBTIMESTAMP2 변환 대상|결과|  
|---------------------------------|------------|  
|DT_FILETIME|소수 자릿수가 DT_FILETIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DATE|DT_DBTIMESTAMP2 데이터 형식이 나타내는 값이 DT_DATE 데이터 형식의 범위를 오버플로하는 경우 DB_E_DATAOVERFLOW 오류가 반환됩니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.<br /><br /> 소수 자릿수가 DT_DATE 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBDATE|DT_DBTIMESTAMP2 데이터 형식이 나타내는 시간 값을 제거합니다.|  
|DT_DBTIME|DT_DBTIMESTAMP2 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIME2|DT_DBTIMESTAMP2 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP2 데이터 형식이 나타내는 값이 DT_DBTIMESTAMP 데이터 형식의 범위를 오버플로하는 경우 DB_E_DATAOVERFLOW 오류를 반환합니다.<br /><br /> DT_DBTIMESTAMP2는 범위가 서기 1년 1월 1일부터 9999년 12월 31일까지인 SQL Server 데이터 형식 datetime2에 매핑됩니다. DT_DBTIMESTAMP는 1753년 1월 1일부터 9999년 12월 31일까지의 보다 작은 범위를 갖는 SQL Server 데이터 형식 datetime에 매핑됩니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMP 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다.<br /><br /> 오류에 대한 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP2|소수 자릿수가 대상 DT_DBTIMESTAMP2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET 데이터 형식의 표준 시간대 필드를 0으로 설정합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMPOFFSET 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>DT_DBTIMESTAMPOFFSET에서 변환  
  
|DT_DBTIMESTAMPOFFSET 변환 대상|결과|  
|--------------------------------------|------------|  
|DT_FILETIME|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC(Coordinated Universal Time)로 변경합니다.<br /><br /> 소수 자릿수가 DT_FILETIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DATE|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC로 변경합니다.<br /><br /> DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 값이 DT_DATE 데이터 형식의 범위를 오버플로하는 경우 DB_E_DATAOVERFLOW 오류를 반환합니다.<br /><br /> 소수 자릿수가 DT_DATE 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다.<br /><br /> 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBDATE|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 날짜 값에 영향을 줄 수 있는 UTC로 변경합니다. 그런 다음 시간 값을 제거합니다.|  
|DT_DBTIME|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC로 변경합니다.<br /><br /> DT_DBTIMESTAMPEOFFSET 데이터 형식이 나타내는 데이터 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIME2|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC로 변경합니다.<br /><br /> DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 날짜 값을 제거합니다.<br /><br /> 소수 자릿수가 DT_DBTIME2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC로 변경합니다.<br /><br /> DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 값이 DT_DBTIMESTAMP 데이터 형식의 범위를 오버플로하는 경우 DB_E_DATAOVERFLOW 오류가 반환됩니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMP 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다.<br /><br /> 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMPOFFSET 데이터 형식이 나타내는 시간 값을 UTC로 변경합니다.<br /><br /> 소수 자릿수가 DT_DBTIMESTAMP2 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
|DT_DBTIMESTAMPOFFSET|소수 자릿수가 대상 DT_DBTIMESTAMPOFFSET 데이터 형식이 포함할 수 있는 소수 자릿수 초의 자릿수를 초과할 경우 소수 자릿수 초 값을 제거합니다. 소수 자릿수 초 값을 제거한 후 이 데이터 잘림에 대한 보고서를 생성합니다. 자세한 내용은 [데이터 오류 처리](../../integration-services/data-flow/error-handling-in-data.md)를 참조하세요.|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>데이터베이스 데이터 형식에 Integration Services 데이터 형식 매핑  
 다음 표에서는 일부 데이터베이스에서 사용되는 데이터 형식을 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 데이터 형식에 매핑하는 데 대한 지침을 제공합니다. 이러한 매핑은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사가 데이터 원본의 데이터를 가져올 때 이 마법사에 사용되는 매핑 파일의 내용을 요약한 것입니다. 이러한 매핑 파일에 대한 자세한 내용은 [SQL Server 가져오기 및 내보내기 마법사](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  이러한 매핑은 엄격하게 일치해야 함을 나타내기 위한 것이 아니라 단지 지침을 제공하기 위한 것입니다. 일부 경우에는 이 표에 표시된 데이터 형식이 아닌 다른 데이터 형식을 사용해야 합니다.  
  
> [!NOTE]  
>  SQL Server 데이터 형식을 사용하여 해당 Integration Services 날짜 및 시간 데이터 형식의 크기를 예상할 수 있습니다.  
  
|데이터 형식|SQL Server<br /><br /> (SQLOLEDB; SQLNCLI10)|SQL Server(SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|Currency||||  
|DT_DATE|||||||  
|DT_DBDATE|[date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[date&#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||날짜|날짜|날짜|  
|DT_DBTIME||||TIMESTAMP|time|Time|  
|DT_DBTIME2|[time&#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[time&#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|||||  
|DT_DBTIMESTAMP|[datetime&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime&#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md), [smalldatetime&#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2&#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset&#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|ssNoversion|ssNoversion|Long||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||BIGINT|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|decimal, numeric|decimal, numeric|  
|DT_R4|REAL|REAL|단일||real|real|  
|DT_R8|float|FLOAT|Double|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|char, varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, 사용자 정의|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 데이터 흐름의 데이터 형식 매핑에 대한 자세한 내용은 [데이터 흐름의 데이터 형식 작업](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)을 참조하세요.  
  
## <a name="related-content"></a>관련 내용  
 blogs.msdn.com의 블로그 항목 - [SSIS 2008의 데이터 형식 변환 기술 간 성능 비교](http://go.microsoft.com/fwlink/?LinkId=220823)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 흐름의 데이터](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
