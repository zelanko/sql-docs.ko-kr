---
title: "상수 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- bit data type
- constants [SQL Server]
- scalar values
- money data type, constants
- binary [SQL Server], constants
- float data type
- Unicode [SQL Server], constants
- constants [Transact-SQL]
- integer constants
- decimal data type, constants
- character strings [SQL Server], constants
- positive values [SQL Server]
- formats [SQL Server], constants
- datetime data type [SQL Server]
- literals [SQL Server], constants
- real data type
- negative values
ms.assetid: 58ae3ff3-b1d5-41b2-9a2f-fc7ab8c83e0e
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d9b212354492b96ca69ebf29afbc39c8ed1de6e3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="constants-transact-sql"></a>상수(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

상수는 리터럴 값 또는 스칼라 값이라고도 하며 특정 데이터 값을 나타내는 기호입니다. 상수의 형식은 나타내는 값의 데이터 형식에 따라 다릅니다.
  
## <a name="character-string-constants"></a>문자열 상수
문자열 상수는 작은따옴표로 묶으며 영숫자(a-z, A-Z, 0-9)와 특수 문자(!, @, 및 #)가 포함됩니다. 데이터 정렬을 지정하는 데 COLLATE 절을 사용하지 않으면 현재 데이터베이스의 기본 데이터 정렬이 문자열 상수에 할당됩니다. 사용자가 입력한 문자열은 컴퓨터의 코드 페이지를 통해 평가되고 필요한 경우 데이터베이스 기본 코드 페이지로 변환됩니다.
  
연결에 대해 QUOTED_IDENTIFIER 옵션이 OFF로 설정된 경우에는 문자열을 큰따옴표로 묶을 수도 있지만 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 제공자와 ODBC 드라이버는 자동으로 SET QUOTED_IDENTIFIER ON을 사용합니다. 작은따옴표를 사용하는 것이 좋습니다.
  
작은따옴표로 묶인 문자열이 삽입된 작은따옴표를 포함하는 경우에 두 개의 작은따옴표가 하나의 작은따옴표를 나타냅니다. 큰따옴표로 묶인 문자열에는 이렇게 하지 않아도 됩니다.
  
다음은 문자열의 예입니다.
  
```sql
'Cincinnati'  
'O''Brien'  
'Process X is 50% complete.'  
'The level for job_id: %d should be between %d and %d.'  
"O'Brien"  
```  
  
빈 문자열은 두 개의 작은따옴표 사이에 아무 것도 없을 경우로 나타냅니다. 6.x 호환성 모드에서 빈 문자열은 하나의 공백으로 처리됩니다.
  
문자열 상수는 고급 데이터 정렬을 지원합니다.
  
> [!NOTE]  
>  로 형식화 되 8000 바이트 보다 큰 문자 상수 **varchar (max)** 데이터입니다.  
  
## <a name="unicode-strings"></a>유니코드 문자열
유니코드 문자열의 형식은 문자열 상수와 비슷하지만 N 식별자로 시작합니다(N은 SQL-92 표준에서 National Language를 나타냄). N 접두사는 대문자여야 합니다. 예를 들어 'Michél' N 'Michél' 유니코드 상수는 문자 상수입니다. 유니코드 상수는 유니코드 데이터로 해석되며 코드 페이지를 사용하여 평가되지 않습니다. 유니코드 상수는 데이터 정렬을 가집니다. 이 데이터 정렬은 주로 비교와 대/소문자 구분을 제어합니다. COLLATE 절을 사용하여 데이터 정렬을 지정하지 않으면 현재 데이터베이스의 기본 데이터 정렬이 유니코드 상수에 할당됩니다. 유니코드 데이터는 문자당 1바이트가 아닌 문자당 2바이트를 사용하여 저장됩니다. 자세한 내용은 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)을 참조하세요.
  
유니코드 문자열 상수는 고급 데이터 정렬을 지원합니다.
  
> [!NOTE]  
>  로 형식화 되 8000 바이트 보다 큰 유니코드 상수 **nvarchar (max)** 데이터입니다.  
  
## <a name="binary-constants"></a>이진 상수
이진 상수는 `0x` 접미사를 가지며 16진수로 구성된 문자열입니다. 이진 상수는 인용 부호로 묶지 않습니다.
  
다음은 이진 문자열의 예입니다.
  
```sql
0xAE  
0x12Ef  
0x69048AEFDD010E  
0x  (empty binary string)  
```  
  
> [!NOTE]  
>  로 형식화 되 8000 바이트 보다 큰 이진 상수 **varbinary (max)** 데이터입니다.  
  
## <a name="bit-constants"></a>비트 상수
**비트** 상수 0 또는 1이 숫자로 표시 되 고 인용 부호로 묶지 않습니다. 1보다 큰 수를 사용하면 1로 변환됩니다.
  
## <a name="datetime-constants"></a>날짜/시간 상수
**날짜/시간** 상수는 특정 형식으로 작은따옴표로 묶인 문자 날짜 값을 사용 하 여 표시 됩니다.
  
다음은 몇 가지 **datetime** 상수:
  
```sql
'December 5, 1985'  
'5 December, 1985'  
'851205'  
'12/5/98'  
```  
  
날짜/시간 상수의 예는:
  
```sql
'14:30:24'  
'04:24 PM'  
```  
  
## <a name="integer-constants"></a>integer 상수
**정수** 상수는 인용 부호로 묶지 않습니다 되며 소수점이 하를 포함 하지 않습니다는 숫자의 문자열에 의해 표시 됩니다. **정수** 상수는 정수 여야 합니다. 않으면 10 진수는 포함할 수 없습니다.
  
다음은 몇 가지 **정수** 상수:
  
```sql
1894  
2  
```  
  
## <a name="decimal-constants"></a>10 진수 상수
**10 진수** 상수는 인용 부호로 묶지 않습니다 및 소수점이 포함 하는 숫자 문자열에 의해 표시 됩니다.
  
다음은 몇 가지 **10 진수** 상수:
  
```sql
1894.1204  
2.0  
```  
  
## <a name="float-and-real-constants"></a>float 및 real 상수
**float** 및 **실제** 상수는 과학적 표기법을 사용 하 여 표시 됩니다.
  
다음은 몇 가지 **float** 또는 **실제** 값:
  
```sql
101.5E5  
0.5E-2  
```  
  
## <a name="money-constants"></a>money 상수
**money** 상수는 선택적인 소수점과 선택적인 통화 기호 접두사를 가진 숫자의 문자열로 표시 됩니다. **money** 상수는 인용 부호로 묶지 묶지 합니다.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 통화를 표시하는 문자열에 세 자릿수마다 쉼표(,)를 넣는 등의 그룹화 규칙을 강제 적용하지 않습니다.
  
> [!NOTE]  
>  쉼표는 지정 된에서 아무 곳 이나 무시 됩니다 **money** 리터럴.  
  
다음은 몇 가지 **money** 상수:
  
```sql
$12  
$542023.14  
```  
  
## <a name="uniqueidentifier-constants"></a>uniqueidentifier 상수
**uniqueidentifier** 상수는 GUID를 나타내는 문자열입니다. 문자 형식이나 이진 문자열 형식으로 지정할 수 있습니다.
  
다음 두 가지 예는 모두 같은 GUID를 지정합니다.
  
```sql
'6F9619FF-8B86-D011-B42D-00C04FC964FF'  
0xff19966f868b11d0b42d00c04fc964ff  
```  
  
## <a name="specifying-negative-and-positive-numbers"></a>양수 및 음수 지정  
지 여부를 나타내는 숫자 양수 또는 음수, 적용 된  **+**  또는  **-**  상수를 하는 단항 연산자입니다. 이렇게 하면 부호 있는 값을 나타내는 숫자 식이 만들어집니다. 숫자 상수 사용 양수는  **+**  또는  **-**  단항 연산자가 적용 되지 않습니다.
  
서명 **정수** 식:  
  
```sql
+145345234
-2147483648
```
서명 **10 진수** 식:  
  
```sql
+145345234.2234
-2147483648.10
```
  
서명 **float** 식:  
  
```sql
+123E-3
-12E5
```
  
서명 **money** 식:  
  
```sql
-$45.56
+$423456.99
```
  
## <a name="enhanced-collations"></a>고급 데이터 정렬  
SQL Server는 고급 데이터 정렬을 지원하는 문자 및 유니코드 문자열 상수를 지원합니다. 자세한 내용은 참조는 [collate&#40; Transact SQL &#41; ](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) 절.
  
## <a name="see-also"></a>참고 항목
[데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[연산자 &#40; Transact SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)
  
  

