---
title: "데이터의 행을 인출 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 142c9a2c95900e5b3776f96d86a145defc447512
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="fetching-a-row-of-data"></a>데이터 행을 인출합니다.
데이터의 행을 인출 하는 응용 프로그램 호출 **SQLFetch**합니다. **SQLFetch** 모든 종류의 커서를 호출할 수 있지만 앞 으로만 이동 가능한 방향으로 행 집합 커서를 이동 합니다. **SQLFetch** 다음 행으로 커서를 이동 하 고 호출 하 여 바인딩된 열에 대 한 데이터를 반환 **SQLBindCol**합니다. 커서는 결과의 끝에 도달 하면 때 설정 **SQLFetch** SQL_NO_DATA를 반환 합니다. 호출에 대 한 예제 **SQLFetch**, 참조 [를 사용 하 여 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)합니다.  
  
 방식을 정확 하 게 **SQLFetch** 구현 되는 드라이버 관련 하지만 일반적인 패턴은 데이터 원본의 열에 바인딩된 모든, 바인딩된 변수로의 형식에 따라 변환 하 고 배치에 대 한 데이터를 검색 하도록 드라이버에 대 한는 이러한 변수의 변환 된 데이터입니다. 드라이버는 데이터를 변환할 수 없는 경우 **SQLFetch** 에서 오류를 반환 합니다. 응용 프로그램의 행을 인출 계속할 수 있지만 현재 행에 대 한 데이터는 손실 됩니다. 바인딩되지 않은 열에 대 한 데이터에 어떤 일이 생기는 드라이버에 따라 달라 지지만 대부분의 드라이버를 검색 하 고 취소 하거나 전혀 검색 되지 않습니다.  
  
 또한 드라이버 연결 되어 있는 모든 길이/표시기 버퍼의 값을 설정 합니다. 열에 대 한 데이터 값이 NULL 이면 드라이버는 해당 길이/표시기 버퍼 SQL_NULL_DATA로 설정 합니다. 데이터 값이 NULL 이면 드라이버는 변환 후에 길이/표시기 버퍼 데이터의 바이트 길이를 설정 합니다. 이 길이 둘 이상의 함수 호출에서 검색 되는 긴 데이터의 경우 처럼 확인할 수 없으면, 드라이버 SQL_NO_TOTAL를 길이/표시기 버퍼를 설정 합니다. 정수 및 날짜 구조에 같은 고정 길이 데이터 형식에 대 한 바이트 길이 데이터 형식의 크기입니다.  
  
 문자 및 이진 데이터와 같은 가변 길이 데이터에 대 한 드라이버는 열에 바인딩된 버퍼의 바이트 길이 대해 변환된 된 데이터의 바이트 길이 확인 에 지정 된 버퍼의 길이 *BufferLength* 인수 **SQLBindCol**합니다. 드라이버는 버퍼에 맞게 데이터를 자릅니다, 그리고 잘리지 않은 길이/표시기 버퍼 길이 SQL_SUCCESS_WITH_INFO를 반환 및 SQLSTATE 01004 (데이터 배치 반환 변환된 된 데이터의 바이트 길이 버퍼의 바이트 길이 보다 큰 경우 진단 프로그램에서 잘립니다). 이 유일한 예외는에서 반환 하는 경우 가변 길이 책갈피 잘립니다 **SQLFetch**, SQLSTATE 22001 (문자열 데이터, 오른쪽이 잘렸습니다)를 반환 하는 합니다.  
  
 고정 길이 데이터를 자를 수 없습니다, 드라이버는 바인딩된 버퍼의 크기는 데이터 형식의 크기 임을 가정 하기 때문에 있습니다. 데이터 잘림 경향이 드물게 응용 프로그램은 일반적으로; 전체 데이터 값을 보유할 수 있을 만큼 큰 버퍼 바인딩합니다 때문에 메타 데이터에서 필요한 크기를 결정 합니다. 그러나 응용 프로그램을 너무 짧게 알고 버퍼를 명시적으로 바인딩할 수 있습니다. 예를 들어, 검색 및 부품 설명의 처음 20 자 또는 긴 텍스트 열의 처음 100 개의 문자로 표시 될 수 있습니다.  
  
 문자 데이터 해야 드라이버에 의해 null로 끝나는 응용 프로그램에 반환 하기 전에 잘린 경우에 합니다. Null 종결 문자는 반환 된 바이트 길이에 포함 되어 있지 않지만 바인딩된 버퍼에 공간이 필요 없습니다. 예를 들어, ASCII 문자 집합의 문자 데이터의 구성 된 문자열을 사용 하 여 응용 프로그램, 드라이버에 반환할 데이터의 50 자 및 응용 프로그램의 버퍼가 25 바이트 길이입니다. 응용 프로그램의 버퍼는 드라이버는 먼저 24 문자 뒤에 null 종결 문자를 반환 합니다. 길이/표시기 버퍼의 바이트 길이 50 반환합니다.  
  
 응용 프로그램 집합을 결과 만드는 문을 실행 하기 전에 SQL_ATTR_MAX_ROWS 문 특성을 설정 하 여 결과 집합의 행 수를 제한할 수 있습니다. 예를 들어, 보고서 서식을 지정 하는 데 사용 하는 응용 프로그램의 미리 보기 모드는 보고서의 첫 번째 페이지를 표시 하려면 충분 한 데이터에만 필요 합니다. 결과 집합의 크기를 제한 하 여 이러한 기능 더 빠르게 실행 됩니다. 이 문 특성은 네트워크 트래픽을 줄이기 위해 되며 모든 드라이버에서 지원 되지 않을 수 있습니다.

