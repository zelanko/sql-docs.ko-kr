---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 708442d30b571f165f7f9d70f346a958764316d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127903"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini 파일(텍스트 파일 드라이버)
텍스트 드라이버를 사용 하는 스키마 정보 파일을 사용 하 여 텍스트 파일의 형식이 결정 됩니다. 스키마 정보 파일을 항상 Schema.ini 라는 이며 항상 텍스트 데이터 원본 동일한 디렉터리에 유지 됩니다. 스키마 정보 파일을 파일, 열 이름 및 데이터 형식 정보 및 기타 여러 데이터 특성의 일반 형식에 대 한 정보를 사용 하 여 IISAM을 제공합니다. Schema.ini 파일은 항상 고정 길이 데이터에 액세스 하기 위한 필수입니다. 날짜/시간, 통화 또는 10 진수 데이터 또는 테이블의 데이터를 처리 하 여 더 많은 제어를 하려는 경우 텍스트 테이블에 포함 된 경우에 Schema.ini 파일을 사용 해야 합니다.  
  
> [!NOTE]  
>  레지스트리에서 Schema.ini에서가 아니라 텍스트 ISAM는 초기 값을 가져옵니다. 모든 새 텍스트 데이터 테이블에 동일한 기본 파일 형식에 적용 됩니다. CREATE TABLE 문에 의해 생성 된 모든 파일의 파일 형식 값을 선택 하 여 설정 되는 이러한 동일한 기본 형식 값을 상속 합니다 **텍스트 형식 정의** 대화 상자를 \<기본 > 합니다 에서선택 **테이블** 목록입니다. Schema.ini 값에서 레지스트리에서 값이 다르면 Schema.ini에서 값으로 레지스트리에서 값을 덮어쓰게 됩니다.  
  
## <a name="understanding-schemaini-files"></a>Schema.ini 파일 이해  
 Schema.ini 파일을 텍스트 파일의 레코드에 대 한 스키마 정보를 제공합니다. 각 Schema.ini 항목 테이블의 다섯 가지 특성 중 하나를 지정 합니다.  
  
-   텍스트 파일 이름  
  
-   파일 형식  
  
-   필드 이름, 너비 및 형식  
  
-   문자 집합  
  
-   특수 데이터 형식 변환  
  
 다음 섹션에서는 이러한 특징을 설명합니다.  
  
## <a name="specifying-the-file-name"></a>파일 이름 지정  
 Schema.ini 첫 번째 항목이 항상 대괄호로 묶인 텍스트 원본 파일의 이름입니다. 다음 예제에서는 Sample.txt 파일에 대 한 항목을 보여 줍니다.  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>파일 형식 지정  
 합니다 **형식** Schema.ini 옵션 텍스트 파일의 형식을 지정 합니다. 텍스트 IISAM 가장 문자 구분 된 파일에서 자동으로 형식을 읽을 수 있습니다. 큰따옴표 (")를 제외 하 고 파일에 구분 기호로 단일 문자를 사용할 수 있습니다. 합니다 **형식** Schema.ini의 설정은 파일 별로 Windows 레지스트리에서 설정을 재정의 합니다. 다음 테이블에 대 한 유효한 값을 나열 합니다 **형식** 옵션입니다.  
  
|형식 지정자|테이블 형식|Schema.ini 형식 문|  
|----------------------|------------------|---------------------------------|  
|**탭으로 구분**|파일의 필드는 탭으로 구분 됩니다.|Format=TabDelimited|  
|**CSV 구분**|파일의 필드는 쉼표 (쉼표로 구분 된 값)으로 구분 됩니다.|형식 = CSVDelimited|  
|**사용자 지정 구분**|파일의 필드 대화 상자에 입력 하려는 모든 문자로 구분 됩니다. 큰따옴표 (")를 제외한 모든 수를 포함 하 여 빈.|형식 = 구분 기호로 분리 됨 (*사용자 지정 문자*)<br /><br /> -또는-<br /><br /> 구분 기호를 사용 하 여 다음을 지정 합니다.<br /><br /> Format=Delimited( )|  
|**고정된 길이**|파일의 필드는 고정된 길이입니다.|Format=FixedLength|  
  
## <a name="specifying-the-fields"></a>필드를 지정합니다.  
 두 가지 방법으로 문자 구분 된 텍스트 파일에 필드 이름을 지정할 수 있습니다.  
  
-   테이블의 첫 번째 행에서 필드 이름을 포함 하 고 설정 **ColNameHeader** 에 **True입니다.**  
  
-   번호로 각 열을 지정 하 고 열 이름과 데이터 형식을 지정 합니다.  
  
 번호로 각 열을 지정 하 고 열 이름, 데이터 형식 및 고정 길이 파일에 대 한 너비를 지정 해야 합니다.  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 재정의에서 설정 합니다 **FirstRowHasNames** 파일 별로 Windows 레지스트리에서 설정 합니다.  
  
 필드의 데이터 형식이 수도 확인할 수 있습니다. 사용 된 **MaxScanRows** 열 형식을 결정할 때 스캔 하는 행 개수를 나타내기 위한 옵션입니다. 설정 하는 경우 **MaxScanRows** 0으로 전체 파일이 검색 됩니다. 합니다 **MaxScanRows** Schema.ini의 설정은 파일 별로 Windows 레지스트리에서 설정을 재정의 합니다.  
  
 다음 항목을 나타내는 Microsoft Jet 필드 이름을 확인 하려면 테이블의 첫 번째 행의 데이터를 사용 해야 하는 데이터를 확인 하려면 전체 파일을 검사 해야 사용 되는 형식:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 열 번호를 사용 하 여 테이블의 필드를 지정 하는 다음 항목 (**Col**_n_) 문자 구분 된 파일에 대 한 선택 사항이 며 고정 길이 파일에 대 한 필수 옵션입니다. 이 예제에서는 두 개의 필드, 10 자 CustomerNumber 텍스트 필드 및 30 자 CustomerName 텍스트 필드에 대 한 Schema.ini 항목을 보여 줍니다.  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 구문의 **Col**_n_ 됩니다.  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Remarks  
 다음 표에서 각 부분을 설명 합니다 **Col**_n_ 항목입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*ColumnName*|텍스트 열의 이름입니다. 열 이름에 공백이 포함 된 경우 큰따옴표로 묶습니다 해야 있습니다.|  
|*type*|데이터 형식 아래와 같습니다.<br /><br /> **Microsoft Jet 데이터 형식**<br /><br /> 비트<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Currency<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> 텍스트 모드<br /><br /> 메모<br /><br /> **ODBC 데이터 형식** Char (텍스트와 동일)<br /><br /> Float (Double과 동일)<br /><br /> 정수 (Short 동일)<br /><br /> LongChar (메모와 동일)<br /><br /> 날짜 *날짜 형식*|  
|**너비**|리터럴 문자열 값 `Width`합니다. 다음 지정 된 열의 너비는 나타냅니다 (문자 구분 된 파일에 대 한 선택적; 고정 길이 파일에 필요).|  
|*#*|열의 너비를 지정 하는 정수 값 (필요한 경우 **너비** 지정).|  
  
## <a name="selecting-a-character-set"></a>문자 집합의 선택  
 두 개의 문자 집합에서 선택할 수 있습니다. ANSI 및 OEM입니다. 합니다 **CharacterSet** Schema.ini의 설정은 파일 별로 Windows 레지스트리에서 설정을 재정의 합니다. 다음 예제에서는 문자 집합을 ANSI 설정 하는 Schema.ini 항목을 보여 줍니다.  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>데이터 유형 형식 지정 및 변환  
 Schema.ini 파일 데이터를 변환 하거나 표시 하는 방법을 지정 하는 데 사용할 수 있는 몇 가지 옵션을 포함 합니다. 다음 표에서 이러한 각 옵션을 나열합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**DateTimeFormat**|날짜 및 시간을 나타내는 형식 문자열을 설정할 수 있습니다. 동일한 형식으로 가져오거나 내보낼 모든 날짜/시간 필드를 처리 하는 경우에이 항목을 지정 해야 합니다. 오전을 제외한 모든 Microsoft Jet 형식 오후 지원 됩니다. 형식 문자열이 없는 경우 Windows 제어판 간단한 날짜 및 시간 옵션이 사용 됩니다.|  
|**DecimalSymbol**|숫자의 소수 부분과에서 정수를 구분 하는 데 사용 되는 모든 단일 문자를 설정할 수 있습니다.|  
|**NumberDigits**|숫자의 소수 부분에 소수 자릿수를 나타냅니다.|  
|**NumberLeadingZeros**|10 진수 값 보다 작거나 1과-1 보다 더; 앞에 오는 0을 포함할지 여부를 지정합니다 이 값일 수 있습니다 하거나 False (선행 0 없음) 또는 True입니다.|  
|**CurrencySymbol**|텍스트 파일에서 통화 값에 사용할 수 있는 통화 기호를 나타냅니다. 달러 기호 ($) 및 Dm을 예로 들 수 있습니다.|  
|**CurrencyPosFormat**|다음 값 중 하나로 설정할 수 있습니다.<br /><br /> -구분 기호가 없는 ($1) 통화 기호 접두사<br />-구분 기호가 없는 통화 기호 접미사 (1$)<br />한 문자 구분 ($ 1)를 사용 하 여 통화 기호 접두사<br />한 문자 구분을 사용 하 여 통화 기호 접미사 (1 $)|  
|**CurrencyDigits**|통화 금액의 소수 부분에 사용 되는 자릿수를 지정 합니다.|  
|**CurrencyNegFormat**|다음 값 중 하나입니다.<br /><br /> -   ($1)<br />-   -$1<br />-   $-1<br />-   $1-<br />-   (1$)<br />-   -1$<br />-   1-$<br />-   1$-<br />-   -1 $<br />-   -$ 1<br />-   1 $-<br />-   $ 1-<br />-   $ -1<br />-   1- $<br />-   ($ 1)<br />-   (1 $)<br /><br /> 이 예제에는 달러 기호를 보여 주지만 적절 한 바꿔야 **CurrencySymbol** 실제 프로그램에는 값입니다.|  
|**CurrencyThousandSymbol**|텍스트 파일의 통화 값을 구분 하 여 사용할 수 있는 단일 문자 기호를 나타냅니다.|  
|**CurrencyDecimalSymbol**|전체 통화 금액의 소수 부분에서 분리 하는 데 사용 되는 모든 단일 문자를 설정할 수 있습니다.|  
  
> [!NOTE]  
>  항목을 생략 하는 경우 Windows 제어판에서 기본 값이 사용 됩니다.
