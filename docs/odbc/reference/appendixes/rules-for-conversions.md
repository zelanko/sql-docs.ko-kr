---
title: 변환에 대 한 규칙 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8020afb215724e05201ac0a2a23ff0f39f1642a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912714"
---
# <a name="rules-for-conversions"></a>변환에 대 한 규칙
숫자 리터럴을 포함 하는 변환은이 섹션의 규칙이 적용 됩니다. 이러한 규칙을 위해 다음 용어 정의 됩니다.  
  
-   *할당 저장:* 를 데이터베이스에서 테이블 열에 데이터를 보낼 때. 에 대 한 호출 중에 상태가 **SQLExecute**, **SQLExecDirect**, 및 **SQLSetPos**합니다. 저장소 할당 하는 동안 데이터베이스 열 "target"을 참조 하 고 "source" 응용 프로그램 버퍼에서 데이터를 의미 합니다.  
  
-   *검색 할당:* 응용 프로그램 버퍼를 데이터베이스에서 데이터를 검색할 때. 에 대 한 호출 중에 상태가 **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, 및 **SQLSetPos**합니다. 검색 할당 하는 동안 "대상" 응용 프로그램 버퍼를 나타내며 "source"은 데이터베이스 열을 나타냅니다.  
  
-   *CS:* 문자 소스 값입니다.  
  
-   *NT:* 숫자 대상의 값입니다.  
  
-   *NS:* 숫자 원본에 있는 값입니다.  
  
-   *CT:* 문자 대상의 값입니다.  
  
-   정확한 숫자 리터럴은 전체 자릿수이 고: 포함 된 자릿수입니다.  
  
-   정확한 숫자 리터럴의의 소수 자릿수: 명시적 또는 묵시적 기간의 오른쪽에 있는 자릿수입니다.  
  
-   근사 숫자 리터럴은 전체 자릿수:의 수의 전체 자릿수입니다.  
  
## <a name="character-source-to-numeric-target"></a>숫자 대상 문자 소스  
 다음은 문자 소스 (CS)에서 숫자 대상 (NT)로 변환 하는 것에 대 한 규칙입니다.  
  
1.  CS CS에 선행 또는 후행 공백을 모두 제거 하 여 얻은 값으로 대체 합니다. CS는 유효 하지 않으면 *숫자 리터럴*, SQLSTATE 22018 (캐스트 사양의 문자 값)이 반환 됩니다.  
  
2.  CS을 소수점 뒤에 0 또는 둘 다 후행 소수점 앞에 선행 0을 제거 하 여 얻은 값으로 바꿉니다.  
  
3.  NT CS 변환 합니다. 유효 자릿수의 손실에 변환 결과가 SQLSTATE 22003 (범위를 벗어났습니다. 숫자 값)이 반환 됩니다. SQLSTATE 01S07 의미 숫자가 손실 변환 결과가 같은 경우 (소수 자릿수 잘림)이 반환 됩니다.  
  
## <a name="numeric-source-to-character-target"></a>문자 숫자 소스  
 다음은 숫자 원본 (NS) 문자 대상 CT ()을 변환 규칙.  
  
1.  LT CT.의 문자에서 길이 사용 합니다. 할당을 위해 검색, LT은이 문자 집합에 대 한 null 종결 문자에서 바이트 수를 뺀 문자에서 버퍼의 길이 같습니다.  
  
2.  경우:  
  
    -   NS 정확한 숫자 형식 이면 YP의 정의를 준수 하는 가장 짧은 문자열 동일 하 게 하 *정확한 숫자-리터럴* YP의 배율은 NS의 소수 자릿수와 동일 하 고 YP의 해석 된 값이 고 NS의 절대 값입니다.  
  
    -   NS 근사 숫자 형식이 면 후자의 경우 나중에 YP 문자열 이어야 합니다.  
  
         사례:  
  
         NS 0 이면 YP은 0입니다.  
  
         YSN 정확한-의 정의를 준수 하는 가장 짧은 문자열을 사용할 수 있도록*숫자 리터럴* 고 해석 된 값이 NS의 절대 값입니다. YSN 길이가 보다 작은 (*정밀도* + 1) 데이터 형식의 NS YP YSN 동일 하 게 하 합니다.  
  
         그렇지 않으면 YP은의 정의를 준수 하는 가장 짧은 문자열 *대략적인 숫자-리터럴* 해석 된 값이 같고 NS의 절대값 *가 수* 이루어져는 단일 *자리* 즉 하지 '0' 뒤에 여는 *기간* 및 *부호 없는 정수*합니다.  
  
3.  사례:  
  
    -   NS 0 보다 작은 경우의 결과 Y의 사용 수 있습니다.  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         여기서 '&#124;&#124;'은 문자열 연결 연산자.  
  
         그렇지 않으면 사용 YP 같은 Y 수 있습니다.  
  
4.  노를 Y의 문자 길이 수 있습니다.  
  
5.  사례:  
  
    -   노 LT 이면 CT Y로 설정 됩니다.  
  
    -   노 LT 보다 작은 경우 다음 CT 설정은 Y 오른쪽에 확장 공백 적절 한 수로 합니다.  
  
         그렇지 않은 경우 (노 > LT), CT.에 Y의 첫 번째 LT 문자를 복사 합니다.  
  
         사례:  
  
         이 저장소 할당, SQLSTATE 22001 (문자열 데이터, 오른쪽이 잘렸습니다) 오류를 반환 합니다.  
  
         검색 할당 경우 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다) 경고를 반환 합니다. 복사 (제외 뒤에 오는 0) 소수 자릿수의 손실에 결과가 경우에 드라이버 정의 된 다음 중 하나가 발생 여부:  
  
         (1) 드라이버 (수 있는 0도) 하는 적절 한 범위로에 Y에 문자열을 자릅니다 고 CT.에 결과 기록  
  
         (2) 드라이버 y에서 문자열 (수 있는 0도) 하는 적절 한 범위로을 반올림 하 고 CT.에 결과 기록  
  
         (3) 드라이버 모두 자릅니다 또는 라운드 했지만 방금 CT.에 Y의 첫 번째 LT 문자를 복사
