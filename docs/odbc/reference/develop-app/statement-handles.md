---
title: 문 핸들 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299679"
---
# <a name="statement-handles"></a>명령문 핸들
*문은* ** \* SELECT FROM Employee**와 같은 SQL 문으로 가장 쉽게 생각할 수 있습니다. 그러나 문은 SQL 문 뿐 이며 문 실행에 사용 되는 문과 매개 변수에 의해 생성 된 결과 집합과 같이 해당 SQL 문과 연결 된 모든 정보로 구성 됩니다. 문에는 응용 프로그램 정의 SQL 문이 없어도 됩니다. 예를 들어 문에 대해 **Sqltables** 와 같은 카탈로그 함수를 실행 하는 경우 테이블 이름 목록을 반환 하는 미리 정의 된 SQL 문을 실행 합니다.  
  
 각 문은 문 핸들로 식별 됩니다. 문은 단일 연결과 연결 되며 해당 연결에 여러 문이 있을 수 있습니다. 일부 드라이버는 지원 되는 활성 문의 수를 제한 합니다. **SQLGetInfo** 의 SQL_MAX_CONCURRENT_ACTIVITIES 옵션은 드라이버가 단일 연결에서 지 원하는 활성 문 수를 지정 합니다. 문이 보류 중인 결과를 포함 하는 경우 (결과가 결과 집합 또는 **INSERT**, **UPDATE**또는 **DELETE** 문의 영향을 받는 행의 수) 또는 **sqlputdata**에 대 한 여러 번의 호출로 데이터가 전송 되는 경우 *활성화* 되도록 정의 됩니다.  
  
 ODBC (드라이버 관리자 또는 드라이버)를 구현 하는 코드 조각 내에서 문 핸들은 다음과 같이 문 정보를 포함 하는 구조를 식별 합니다.  
  
-   문의 상태  
  
-   현재 문 수준 진단  
  
-   문의 매개 변수 및 결과 집합 열에 바인딩된 응용 프로그램 변수의 주소  
  
-   각 문 특성의 현재 설정입니다.  
  
 문 핸들은 대부분의 ODBC 함수에서 사용 됩니다. 특히 매개 변수 및 결과 집합 열 (**SQLBindParameter** 및 **SQLBindCol**)을 바인딩하고, 문 (**Sqlprepare**, **sqlprepare**및 **sqlexecdirect**)을 바인딩하고 실행 하 고, 메타 데이터 (**sqlcolattribute** 및 **SQLDescribeCol**)를 검색 하 고, 결과를 인출 (**sqlprepare**) 하 고, 진단 (**SQLGetDiagField** 및 **SQLGetDiagRec**)을 검색 하는 함수에 사용 됩니다. 또한 카탈로그 함수 (**Sqlcolumns**, **sqlcolumns**등)와 여러 다른 함수에서 사용 됩니다.  
  
 문 핸들은 **SQLAllocHandle** 를 사용 하 여 할당 되 고 **sqlfreehandle**을 사용 하 여 해제 됩니다.
