---
title: 변환에 대 한 규칙 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706101"
---
# <a name="rules-for-conversions"></a>변환에 대한 규칙
이 섹션의 규칙은 숫자 리터럴을 포함 하는 변환에 적용 됩니다. 이러한 규칙을 위해 다음 조건에 정의 됩니다.  
  
-   *할당 저장:* 데이터베이스의 테이블 열으로 데이터를 보낼 때. 호출 하는 동안 이런 **SQLExecute**를 **SQLExecDirect**, 및 **SQLSetPos**합니다. 저장소 할당 하는 동안 데이터베이스 열 "target"을 참조 하 고 "source" 응용 프로그램 버퍼의 데이터를 가리킵니다.  
  
-   *검색 할당:* 응용 프로그램 버퍼를 데이터베이스에서 데이터를 검색할 때. 호출 하는 동안 이런 **SQLFetch**, **SQLGetData**합니다 **SQLFetchScroll**, 및 **SQLSetPos**합니다. 검색 할당 하는 동안 "target" 응용 프로그램 버퍼를 나타내며 "source" 데이터베이스 열을 가리킵니다.  
  
-   *CS:* 문자 소스 값입니다.  
  
-   *NT:* 숫자 대상의 값입니다.  
  
-   *NS:* 숫자 원본 값입니다.  
  
-   *CT:* 문자 대상의 값입니다.  
  
-   정확한 숫자 리터럴은 전체 자릿수: 포함 하는 자릿수입니다.  
  
-   정확한 숫자 리터럴의 크기: 명시적 또는 묵시적 기간의 오른쪽 자릿수입니다.  
  
-   대략적인 숫자 리터럴은 전체 자릿수: 전체 자릿수는가 수입니다.  
  
## <a name="character-source-to-numeric-target"></a>문자 소스에서 숫자 대상  
 다음은 문자 소스 (CS)에서 숫자 대상 (NT)로 변환 하는 것에 대 한 규칙:  
  
1.  CS CS에 선행 또는 후행 공백을 제거 하 여 가져온 값으로 대체 합니다. CS는 유효 하지 않으면 *숫자 리터럴*, SQLSTATE 22018 (캐스트 사양의 문자 값)이 반환 됩니다.  
  
2.  CS 소수점 뒤에 0 또는 둘 다 후행 소수점 앞에 선행 0을 제거 하 여 가져온 값으로 대체 합니다.  
  
3.  CS NT 변환 합니다. 변환 결과 유효 자릿수의 손실에서, SQLSTATE 22003 (범위를 벗어났습니다. 숫자 값)이 반환 됩니다. 변환 결과 SQLSTATE 01S07 의미 자릿수 손실에서 하는 경우 (소수 잘림)이 반환 됩니다.  
  
## <a name="numeric-source-to-character-target"></a>숫자 소스에서 문자 대상  
 다음은 숫자 원본 (NS)에서 문자 대상 (CT)을 변환 하기 위한 규칙.  
  
1.  LT을 CT.의 문자에서 길이 수 있습니다. 할당을 위해 검색, LT이 문자 집합에 대 한 null 종료 문자는 바이트 수를 빼기 문자에서 버퍼의 길이 같을 경우합니다  
  
2.  사례:  
  
    -   YP의 정의 준수 하는 가장 짧은 문자열을 동일 하면 NS 정확한 숫자 형식 이면 *정확한 숫자-리터럴* YP 규모 NS의 소수 자릿수와 동일 하 고 YP 해석 된 값이 되도록 합니다 NS의 절대 값입니다.  
  
    -   NS 근사치 숫자 형식 인 경우 문자열을 다음과 같이 수 YP 하면:  
  
         사례:  
  
         NS 0 이면 YP은 0입니다.  
  
         YSN 정확한-정의 준수 하는 가장 짧은 문자열을 사용할 수 있도록*숫자 리터럴* 고 해석 된 값이 NS의 절대 값입니다. YSN 길이인 경우 보다 작은 (*정밀도* + 1) NS의 데이터 형식, 그러면 YP YSN 동일 합니다.  
  
         YP의 정의 준수 하는 가장 짧은 문자열을가 하는 고, 그렇지 *대략적인 숫자-리터럴* 해석 된 값인 NS 및 해당의 절대 값인 *가* 이루어져를 단일 *자리* 즉 하지 '0' 뒤에 *기간* 와 *부호 없는 정수*합니다.  
  
3.  사례:  
  
    -   NS 0 보다 작은 경우의 결과 Y 하면:  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         여기서 '&#124;&#124;'은 문자열 연결 연산자.  
  
         그렇지 않으면 Y를 YP 같은 사용 수 있습니다.  
  
4.  LY를 Y의 문자에서 길이 사용할 수 있습니다.  
  
5.  사례:  
  
    -   LY LT 같으면 CT은 Y로 설정 합니다.  
  
    -   LY LT 보다 작은 경우, 다음 CT Y로 설정 된 오른쪽에 확장 공간의 적절 한 수로 합니다.  
  
         그렇지 않은 경우 (LY > LT), CT. Y의 첫 번째 LT 문자 복사  
  
         사례:  
  
         저장소 할당 인 경우 SQLSTATE 22001 (문자열 데이터, 오른쪽이 잘렸습니다) 오류를 반환 합니다.  
  
         검색 할당 인 경우 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다) 경고를 반환 합니다. 복사 (뒤에 오는 0) 이외의 소수 자릿수의 손실에 결과가 때 드라이버에서 정의 된 다음 중 하나가 발생 여부:  
  
         (1) 드라이버 (해당 되는 0도) 적절 한 확장에 y-축으로 문자열을 자릅니다 및 CT.에 결과 씁니다.  
  
         (2) 드라이버 (해당 되는 0도) 적절 한 확장에 Y는 문자열을 반올림 하 고 결과 CT. 씁니다.  
  
         (3) 드라이버 모두 자릅니다 나 라운드 있지만 CT. Y의 첫 번째 LT 문자를 복사만
