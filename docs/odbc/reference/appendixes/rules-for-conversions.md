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
ms.openlocfilehash: 9ca64355a80ce8892f0ea0494e165d934d8d7a88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057095"
---
# <a name="rules-for-conversions"></a>변환에 대한 규칙
이 단원의 규칙은 숫자 리터럴을 포함 하는 변환에 적용 됩니다. 이러한 규칙의 목적에 따라 다음과 같은 용어가 정의 됩니다.  
  
-   *저장소 할당:* 데이터베이스의 테이블 열에 데이터를 보내는 경우 이는 **Sqlexecute**, **Sqlexecdirect**및 **SQLSetPos**를 호출 하는 동안 발생 합니다. 저장소 할당 중 "대상"은 데이터베이스 열을 나타내고 "source"는 응용 프로그램 버퍼의 데이터를 참조 합니다.  
  
-   *검색 할당:* 데이터베이스에서 응용 프로그램 버퍼로 데이터를 검색 하는 경우 이는 **Sqlfetch**, **SQLGetData**, **sqlfetchscroll**및 **SQLSetPos**를 호출 하는 동안 발생 합니다. 검색 할당 중 "대상"은 응용 프로그램 버퍼를 나타내고 "source"는 데이터베이스 열을 나타냅니다.  
  
-   *CS:* 문자 소스에 있는 값입니다.  
  
-   *NT:* 숫자 대상의 값입니다.  
  
-   *NS:* 숫자 원본에 있는 값입니다.  
  
-   *CT:* 문자 대상의 값입니다.  
  
-   정확한 숫자 리터럴의 전체 자릿수입니다. 여기에 포함 된 자릿수입니다.  
  
-   정확한 숫자 리터럴의 소수 자릿수입니다. 표시 되거나 암시 된 기간의 오른쪽에 있는 자릿수입니다.  
  
-   근사 숫자 리터럴의 전체 자릿수입니다. 해당 양의 자릿수입니다.  
  
## <a name="character-source-to-numeric-target"></a>문자 소스에서 숫자 대상으로  
 문자 원본 (CS)에서 숫자 대상 (NT)으로 변환 하는 규칙은 다음과 같습니다.  
  
1.  Cs는 CS에서 선행 또는 후행 공백을 제거 하 여 가져온 값으로 바꿉니다. CS가 유효한 *숫자 리터럴이*아니면 SQLSTATE 22018 (캐스트 사양에 잘못 된 문자 값)이 반환 됩니다.  
  
2.  CS는 소수점 앞에 오는 0을 제거 하 고 소수점 뒤에 후행 0을 제거 하거나 둘 다 제거 하 여 얻은 값으로 대체 합니다.  
  
3.  CS를 NT로 변환 합니다. 변환 결과 유효 자릿수가 손실 되 면 SQLSTATE 22003 (범위를 벗어난 숫자 값)이 반환 됩니다. 변환으로 인해 유효 하지 않은 자릿수가 손실 되는 경우 SQLSTATE 01S07 (소수 잘림)이 반환 됩니다.  
  
## <a name="numeric-source-to-character-target"></a>숫자 소스에서 문자 대상으로  
 다음은 숫자 원본 (NS)에서 문자 대상 (CT)으로 변환 하는 규칙입니다.  
  
1.  CT의 문자 길이를 사용 합니다. 검색 할당의 경우이 문자 집합의 null 종료 문자에서 바이트 수를 뺀 문자 단위의 버퍼 길이와 동일 합니다.  
  
2.  경우  
  
    -   NS가 정확한 숫자 형식이 면 YP의 소수 자릿수가 NS의 소수 자릿수와 동일 하 게 하는 *정확한 숫자 리터럴의* 정의를 준수 하는 가장 짧은 문자열 및 yp의 해석 된 값이 ns의 절대값입니다.  
  
    -   NS가 근사 숫자 형식이 면 다음과 같이 YP를 문자열로 지정 합니다.  
  
         사례:  
  
         NS가 0과 같으면 YP는 0입니다.  
  
         YSN은 정확한*숫자 리터럴의* 정의를 준수 하 고 해석 된 값이 NS의 절대값 인 최단 문자열입니다. YSN의 길이가 데이터 형식의 NS의 (*전체 자릿수* + 1) 보다 작은 경우 YP는 ysn을 사용 합니다.  
  
         그렇지 않은 경우 YP는 해석 된 값이 NS의 절대값이 고,가 ' 0 '이 아닌 단일 *자릿수로* 구성 된 *근사 숫자 리터럴의* 정의를 준수 하는 최단 문자열입니다 *. 그 다음* 에는 *마침표* 와 *부호 없는 정수가*나옵니다.  
  
3.  사례:  
  
    -   NS가 0 보다 작은 경우 Y의 결과는 다음과 같습니다.  
  
         '-'  &#124;&#124; YP  
  
         여기서 ' &#124;&#124; '는 문자열 연결 연산자입니다.  
  
         그렇지 않으면 Y가 YP와 동일 합니다.  
  
4.  Y의 문자 길이를 사용 합니다.  
  
5.  사례:  
  
    -   이와 같은 경우에는 CT가 Y로 설정 됩니다.  
  
    -   매우 작은 경우에는 적절 한 공백 수 만큼 오른쪽에서 CT가 Y로 확장 되도록 설정 됩니다.  
  
         그렇지 않고 (매우 > LT) Y의 첫 번째 LT 문자를 CT로 복사 합니다.  
  
         사례:  
  
         저장소 할당 인 경우에는 SQLSTATE 22001 (문자열 데이터, 오른쪽 잘림) 오류를 반환 합니다.  
  
         검색 할당 인 경우에는 SQLSTATE 01004 (문자열 데이터, 오른쪽 잘림) 경고를 반환 합니다. 복사할 때 후행 0이 아닌 소수 자릿수가 손실 되 면 다음 중 하나가 발생 하는지 여부에 따라 드라이버가 정의 됩니다.  
  
         (1) 드라이버는 Y의 문자열을 적절 한 소수 자릿수 (0 일 수 있음)로 자르고 결과를 CT에 씁니다.  
  
         (2) 드라이버는 Y의 문자열을 적절 한 배율 (0 일 수 있음)으로 반올림 하 고 결과를 CT에 씁니다.  
  
         (3) 드라이버는 자르거나 라운드 하지 않고 Y의 첫 번째 LT 문자를 CT로 복사 합니다.
