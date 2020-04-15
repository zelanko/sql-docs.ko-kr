---
title: 전환 규칙 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305089"
---
# <a name="rules-for-conversions"></a>변환에 대한 규칙
이 섹션의 규칙은 숫자 리터럴과 관련된 변환에 적용됩니다. 이러한 규칙의 목적을 위해 다음 용어가 정의됩니다.  
  
-   *저장 할당:* 데이터베이스의 테이블 열로 데이터를 보낼 때 이 문제는 **SQLExecute,** **SQLExecDirect**및 **SQLSetPos를**호출하는 동안 발생합니다. 저장소 할당 중에 "대상"은 데이터베이스 열을 참조하고 "원본"은 응용 프로그램 버퍼의 데이터를 참조합니다.  
  
-   *검색 할당:* 데이터베이스에서 응용 프로그램 버퍼로 데이터를 검색할 때 이 문제는 **SQLFetch,** **SQLGetData,** **SQLFetchScroll**및 **SQLSetPos를**호출하는 동안 발생합니다. 검색 할당 중에 "대상"은 응용 프로그램 버퍼를 참조하고 "원본"은 데이터베이스 열을 참조합니다.  
  
-   *CS:* 문자 소스의 값입니다.  
  
-   *NT:* 숫자 대상의 값입니다.  
  
-   *NS:* 숫자 소스의 값입니다.  
  
-   *CT:* 문자 대상의 값입니다.  
  
-   정확한 숫자 리터럴의 정밀도: 포함된 숫자 수입니다.  
  
-   정확한 숫자 리터럴의 배율: 표현또는 묵시적 기간의 오른쪽에 있는 숫자 수입니다.  
  
-   대략적인 숫자 리터럴의 정밀도: 사마의 정밀도.  
  
## <a name="character-source-to-numeric-target"></a>숫자 대상에 문자 소스  
 다음은 문자 소스(CS)에서 숫자 대상(NT)으로 변환하는 규칙입니다.  
  
1.  CS의 행간 또는 후행 공백을 제거하여 얻은 값으로 CS를 바꿉니다. CS가 유효한 *숫자 리터럴이*아닌 경우 SQLSTATE 22018(캐스트 사양에 대해 잘못된 문자 값)이 반환됩니다.  
  
2.  소수점 앞에 선행 영점을 제거하고 소수점 다음으로 0을 따라가거나 둘 다를 제거하여 얻은 값으로 CS를 바꿉니다.  
  
3.  CS를 NT로 변환합니다. 변환으로 인해 상당한 자릿수가 손실되면 SQLSTATE 22003(범위를 벗어난 숫자 값)이 반환됩니다. 변환으로 인해 중요하지 않은 자릿수가 손실되면 SQLSTATE 01S07(분수 잘림)이 반환됩니다.  
  
## <a name="numeric-source-to-character-target"></a>문자 대상에 대한 숫자 소스  
 다음은 숫자 소스(NS)에서 문자 대상(CT)으로 변환하는 규칙입니다.  
  
1.  LT를 CT 문자의 길이가 되게 합니다. 검색 할당의 경우 LT는 이 문자 집합의 null-termination 문자의 바이트 수를 뺀 문자의 버퍼 길이와 같습니다.  
  
2.  경우:  
  
    -   NS가 정확한 숫자 형식인 경우 YP의 배율이 NS의 배율과 같고 YP의 해석 값이 NS의 절대 값인 지 정확히 *숫자-리터럴의* 정의를 따르는 가장 짧은 문자 문자열과 YP를 같게 합니다.  
  
    -   NS가 대략적인 숫자 형식인 경우 YP를 다음과 같이 문자 문자열로 지정합니다.  
  
         사례:  
  
         NS가 0이면 YP는 0입니다.  
  
         YSN은 정확한*숫자-리터럴의* 정의를 준수하고 해석 값이 NS의 절대 값인 가장 짧은 문자 문자열이 되도록 합니다. YSN의 길이가 NS의 데이터*형식(정밀도* + 1)보다 적으면 YP가 YSN과 같게 합니다.  
  
         그렇지 않으면 YP는 해석 값이 NS의 절대 값이며 *mantissa가* '0'이 아닌 한 *자리로* 구성되고 *마침표와* *서명되지 않은 정수다음에*있는 *근사 숫자-리터럴의* 정의를 준수하는 가장 짧은 문자 문자열입니다.  
  
3.  사례:  
  
    -   NS가 0보다 크면 Y가 다음의 결과를 보자:  
  
         '-' &#124;&#124; YP  
  
         여기서 '&#124;&#124;'은 문자열 연결 연산자입니다.  
  
         그렇지 않으면 Y가 YP와 같게 합니다.  
  
4.  LY가 Y문자의 길이가 되게 합니다.  
  
5.  사례:  
  
    -   LY가 LT와 같으면 CT가 Y로 설정됩니다.  
  
    -   LY가 LT보다 적으면 CT는 적절한 수의 공백으로 오른쪽에 있는 Y로 확장됩니다.  
  
         그렇지 않으면 (LY > LT) CT에 Y의 첫 번째 LT 문자를 복사합니다.  
  
         사례:  
  
         저장소 할당인 경우 SQLSTATE 22001(문자열 데이터, 오른쪽 잘린)을 반환합니다.  
  
         검색 할당인 경우 SQLSTATE 01004 경고(문자열 데이터, 오른쪽 잘린)를 반환합니다. 복사본으로 인해 소수 자릿수가 손실되는 경우(후행 영점 제외) 다음 중 하나가 발생하는지 여부가 드라이버 정의됩니다.  
  
         (1) 드라이버는 Y의 문자열을 적절한 축척(0이 될 수도 있음)으로 트렁크하고 결과를 CT에 씁니다.  
  
         (2) 드라이버는 Y의 문자열을 적절한 축척으로 반올림하고(0이 될 수도 있음) 결과를 CT에 씁니다.  
  
         (3) 드라이버는 자이나 라운드를 하지 않고 Y의 첫 번째 LT 문자를 CT에 복사합니다.
