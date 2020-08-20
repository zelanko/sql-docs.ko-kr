---
description: Schema.ini 파일(텍스트 파일 드라이버)
title: Schema.ini 파일 (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b4bbebfa6eb184bf81cba4a9faf5e3200f428de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500226"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 파일(텍스트 파일 드라이버)
텍스트 드라이버를 사용 하는 경우 텍스트 파일의 형식은 스키마 정보 파일을 사용 하 여 결정 됩니다. 스키마 정보 파일은 항상 Schema.ini 이름이 지정 되며 항상 텍스트 데이터 원본과 동일한 디렉터리에 보관 됩니다. 스키마 정보 파일은 파일의 일반 형식, 열 이름 및 데이터 형식 정보 및 기타 여러 데이터 특성에 대 한 정보를 IISAM에 제공 합니다. 고정 길이 데이터에 액세스 하려면 항상 Schema.ini 파일이 필요 합니다. 텍스트 테이블에 DateTime, Currency 또는 Decimal 데이터가 포함 되어 있거나 테이블의 데이터 처리에 대 한 더 많은 제어가 필요한 경우에는 Schema.ini 파일을 사용 해야 합니다.  
  
> [!NOTE]  
>  텍스트 ISAM은 Schema.ini 아니라 레지스트리에서 초기 값을 가져옵니다. 동일한 기본 파일 형식이 모든 새 텍스트 데이터 테이블에 적용 됩니다. CREATE TABLE 문으로 만든 모든 파일은 동일한 기본 형식 값을 상속 하며,이 값은 테이블 목록에서 선택한 **텍스트 형식 정의** 대화 상자에서 파일 형식 값을 선택 하 여 설정 합니다 \<default> **Tables** . 레지스트리의 값이 Schema.ini의 값과 다를 경우 레지스트리의 값을 Schema.ini 값으로 덮어씁니다.  
  
## <a name="understanding-schemaini-files"></a>Schema.ini 파일 이해  
 Schema.ini 파일은 텍스트 파일에서 레코드에 대 한 스키마 정보를 제공 합니다. 각 Schema.ini 항목은 테이블의 다섯 가지 특성 중 하나를 지정 합니다.  
  
-   텍스트 파일 이름입니다.  
  
-   파일 형식  
  
-   필드 이름, 너비 및 형식  
  
-   문자 집합입니다.  
  
-   특수 데이터 형식 변환  
  
 다음 섹션에서는 이러한 특성에 대해 설명 합니다.  
  
## <a name="specifying-the-file-name"></a>파일 이름 지정  
 Schema.ini의 첫 번째 항목은 항상 대괄호로 묶은 텍스트 소스 파일의 이름입니다. 다음 예에서는 Sample.txt 파일의 항목을 보여 줍니다.  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>파일 형식 지정  
 Schema.ini의 **format** 옵션은 텍스트 파일의 형식을 지정 합니다. 텍스트 IISAM는 대부분의 문자 구분 파일에서 서식을 자동으로 읽을 수 있습니다. 큰따옴표 (")를 제외한 모든 단일 문자를 파일에서 구분 기호로 사용할 수 있습니다. Schema.ini의 **형식** 설정은 파일을 기준으로 Windows 레지스트리의 설정을 재정의 합니다. 다음 표에서는 **Format** 옵션에 대 한 유효한 값을 나열 합니다.  
  
|형식 지정자|테이블 형식|Schema.ini Format 문|  
|----------------------|------------------|---------------------------------|  
|**탭으로 구분**|파일의 필드는 탭으로 구분 됩니다.|Format = TabDelimited|  
|**CSV 구분**|파일의 필드는 쉼표로 구분 된 값으로 구분 됩니다.|Format = CSVDelimited|  
|**사용자 지정 구분**|파일의 필드는 대화 상자에 입력 하도록 선택한 문자로 구분 됩니다. 공백을 포함 하 여 큰따옴표 (")를 제외한 모든를 사용할 수 있습니다.|Format = 구분 기호로 분리 됨 (*사용자 지정 문자*)<br /><br /> 또는<br /><br /> 구분 기호를 지정 하지 않음:<br /><br /> Format = 구분 기호로 분리 됨 ()|  
|**고정 길이**|파일의 필드 길이가 고정 되어 있습니다.|Format = FixedLength|  
  
## <a name="specifying-the-fields"></a>필드 지정  
 다음 두 가지 방법으로 문자 구분 텍스트 파일에 필드 이름을 지정할 수 있습니다.  
  
-   테이블의 첫 번째 행에 필드 이름을 포함 하 고 **Colnameheader** 를 True로 설정 **합니다.**  
  
-   각 열을 번호로 지정 하 고 열 이름과 데이터 형식을 지정 합니다.  
  
 각 열을 번호로 지정 하 고 고정 길이 파일의 열 이름, 데이터 형식 및 너비를 지정 해야 합니다.  
  
> [!NOTE]  
>  Schema.ini의 **Colnameheader** 설정은 Windows 레지스트리의 파일 **FirstRowHasNames** 설정을 재정의 합니다.  
  
 필드의 데이터 형식을 확인할 수도 있습니다. **MaxScanRows** 옵션을 사용 하 여 열 유형을 결정할 때 검색할 행 수를 지정할 수 있습니다. **MaxScanRows** 를 0으로 설정 하면 전체 파일이 검색 됩니다. Schema.ini의 **MaxScanRows** 설정은 Windows 레지스트리, 파일 별로 파일의 설정을 재정의 합니다.  
  
 다음 항목은 Microsoft Jet가 테이블의 첫 번째 행에 있는 데이터를 사용 하 여 필드 이름을 확인 하 고 전체 파일을 검사 하 여 사용 되는 데이터 형식을 확인 해야 함을 나타냅니다.  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 다음 항목은 문자 구분 파일의 경우 선택 사항이 고 고정 길이 파일에 필요한 열 번호 (**Col**_n_) 옵션을 사용 하 여 테이블의 필드를 지정 합니다. 이 예에서는 10 자의 CustomerNumber 텍스트 필드와 30 자 CustomerName 텍스트 필드의 두 필드에 대 한 Schema.ini 항목을 보여 줍니다.  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 **Col**_n_ 의 구문은 다음과 같습니다.  
  
```  
  
n=ColumnName type [Width] [#]  
```  
  
## <a name="remarks"></a>설명  
 다음 표에서는 **Col**_n_ 항목의 각 부분에 대해 설명 합니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*ColumnName*|열의 텍스트 이름입니다. 열 이름에 공백이 포함 된 경우에는 큰따옴표로 묶어야 합니다.|  
|*type*|데이터 형식은 다음과 같습니다.<br /><br /> **Microsoft Jet 데이터 형식**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> 통화<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> 텍스트<br /><br /> 메모<br /><br /> **ODBC 데이터 형식** Char (텍스트와 동일)<br /><br /> Float (Double과 같음)<br /><br /> Integer (Short와 동일)<br /><br /> 이상 문자 (메모와 동일)<br /><br /> 날짜 *날짜 형식*|  
|**Width**|리터럴 문자열 값 `Width` 입니다. 다음 숫자가 열 너비를 지정 함을 나타냅니다. 문자 구분 파일의 경우 선택 사항이 며 고정 길이 파일에 필요 합니다.|  
|*#*|열의 너비를 지정 하는 정수 값입니다 ( **width** 가 지정 된 경우 필수).|  
  
## <a name="selecting-a-character-set"></a>문자 집합 선택  
 ANSI와 OEM의 두 문자 집합 중에서 선택할 수 있습니다. Schema.ini의 **CharacterSet** 설정은 Windows 레지스트리, 파일 별로 파일의 설정을 재정의 합니다. 다음 예제에서는 문자 집합을 ANSI로 설정 하는 Schema.ini 항목을 보여 줍니다.  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>데이터 형식 형식 및 변환 지정  
 Schema.ini 파일에는 데이터를 변환 하거나 표시 하는 방법을 지정 하는 데 사용할 수 있는 몇 가지 옵션이 포함 되어 있습니다. 다음 표에서는 이러한 각 옵션을 보여 줍니다.  
  
|옵션|설명|  
|------------|-----------------|  
|**DateTimeFormat**|날짜 및 시간을 나타내는 형식 문자열로 설정 될 수 있습니다. 가져오기/내보내기의 모든 날짜/시간 필드가 동일한 형식으로 처리 되는 경우이 항목을 지정 해야 합니다. A.M.를 제외한 모든 Microsoft Jet 형식 오후 시간이 모두 이 지원됩니다. 서식 문자열이 없으면 Windows 제어판의 짧은 날짜 및 시간 옵션이 사용 됩니다.|  
|**DecimalSymbol**|는 숫자의 소수 부분에서 정수를 구분 하는 데 사용 되는 단일 문자로 설정할 수 있습니다.|  
|**숫자 숫자**|숫자의 소수 부분에 있는 10 진수 자릿수를 나타냅니다.|  
|**NumberLeadingZeros**|1 보다 작은 10 진수 값에 선행 0이 포함 되어야 하는지 여부를 지정 합니다. 이 값은 False (앞에 오는 0 없음) 또는 True 일 수 있습니다.|  
|**CurrencySymbol**|텍스트 파일의 통화 값에 사용할 수 있는 통화 기호를 나타냅니다. 예로는 달러 기호 ($) 및 Dm이 있습니다.|  
|**CurrencyPosFormat**|는 다음 값 중 하나로 설정할 수 있습니다.<br /><br /> -구분 없이 통화 기호 접두사 ($1)<br />-구분 없이 통화 기호 접미사 ($1)<br />-문자 구분이 하나인 통화 기호 접두사 ($1)<br />-문자 구분이 하나인 통화 기호 접미사 ($1)|  
|**CurrencyDigits**|통화 금액의 소수 부분에 사용 되는 자릿수를 지정 합니다.|  
|**CurrencyNegFormat**|다음 값 중 하나일 수 있습니다.<br /><br /> -($1)<br />--$1<br />-$-1<br />-$1-<br />-($1)<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />-($1)<br />-($1)<br /><br /> 이 예제는 달러 기호를 보여 주지만 실제 프로그램에서 적절 한 **CurrencySymbol** 값으로 바꾸어야 합니다.|  
|**CurrencyThousandSymbol**|텍스트 파일의 통화 값을 천 단위로 구분 하는 데 사용할 수 있는 단일 문자 기호를 나타냅니다.|  
|**CurrencyDecimalSymbol**|통화 금액의 소수 부분에서 전체를 구분 하는 데 사용 되는 단일 문자로 설정할 수 있습니다.|  
  
> [!NOTE]  
>  항목을 생략 하면 Windows 제어판의 기본값이 사용 됩니다.
