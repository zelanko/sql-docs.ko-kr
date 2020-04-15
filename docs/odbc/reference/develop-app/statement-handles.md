---
title: 명령문 핸들 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 65d6d78b-a8c8-489a-9dad-f8d127a44882
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1be90fe10d10a0b087d1c9724fed249805eb4dba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299679"
---
# <a name="statement-handles"></a>명령문 핸들
*문은* **직원 에서 SELECT와 \* **같은 SQL 문으로 가장 쉽게 생각됩니다. 그러나 문은 SQL 문 그 이상입니다 - 명령문 실행에 사용되는 명령문 및 매개 변수에 의해 생성된 모든 결과 집합과 같이 해당 SQL 문과 연결된 모든 정보로 구성됩니다. 문에는 응용 프로그램 정의 SQL 문이 있을 필요도 없습니다. 예를 들어 **SQLTable과** 같은 카탈로그 함수가 명령문에서 실행되면 테이블 이름 목록을 반환하는 미리 정의된 SQL 문을 실행합니다.  
  
 각 문은 문 핸들에 의해 식별됩니다. 문은 단일 연결과 연결되며 해당 연결에 여러 문이 있을 수 있습니다. 일부 드라이버는 지원하는 활성 문의 수를 제한합니다. **SQLGetInfo의** SQL_MAX_CONCURRENT_ACTIVITIES 옵션은 드라이버가 단일 연결에서 지원하는 활성 문의 수를 지정합니다. 결과가 보류 중이거나 결과가 결과 집합이거나 **INSERT,** **UPDATE**또는 **DELETE** 문의 영향을 받는 행 수가 있거나 **데이터가 SQLPutData**에 대한 여러 호출로 전송되는 경우 문이 *활성* 상태로 정의됩니다.  
  
 ODBC(드라이버 관리자 또는 드라이버)를 구현하는 코드 조각 내에서 문 핸들은 다음과 같은 명령문 정보를 포함하는 구조를 식별합니다.  
  
-   명령문의 상태  
  
-   현재 명령문 수준 진단  
  
-   명령문의 매개 변수 및 결과 집합 열에 바인딩된 응용 프로그램 변수의 주소  
  
-   각 문 특성의 현재 설정  
  
 명령문 핸들은 대부분의 ODBC 함수에서 사용됩니다. 특히 함수에서 매개 변수 및 결과 집합**열(SQLBindParameter** 및 **SQLBindCol),** 준비 및 실행 문(SQLPrepare , **SQLExecute****SQLPrepare**및 **SQLExecDirect),** 메타데이터**검색(SQLColAttribute** 및 **SQLDescribeCol),** 결과(SQLGetDiagField 및 SQLGetDiagRec) 및 검색**SQLFetch****진단(SQLGetDiagField** 및 **SQLGetDiagRec)을**입력합니다. 또한 카탈로그**함수(SQLColumns,** **SQLTables**등)와 여러 다른 함수에도 사용됩니다.  
  
 명령문 핸들은 **SQLAllocHandle으로** 할당되고 **SQLFreeHandle**을 통해 해제됩니다.
