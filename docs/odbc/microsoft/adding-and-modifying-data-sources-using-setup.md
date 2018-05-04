---
title: 설치 프로그램을 사용 하 여 데이터 추가 및 수정 원본 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61fd7c284be951d8dfd6389b79df80d6b3f11334
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>추가 하 고 설치를 사용 하 여 데이터 원본 수정
> [!IMPORTANT]  
>  이 기능은 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. Oracle에서 제공 하는 ODBC 드라이버를 사용 하십시오.  
  
 네트워크 라이브러리, 서버, 데이터베이스 및 기타 특성을 포함할 수 있는 데이터에 대 한 경로 식별 하는 데이터 원본-이 경우 데이터 원본이 Oracle 데이터베이스의 경로입니다. 데이터 원본에 연결할 드라이버 관리자는 특정 연결 정보에 대 한 Windows 레지스트리를 확인 합니다.  
  
 ODBC 데이터 원본 관리자가 만든 레지스트리 항목은 ODBC 드라이버 관리자와 ODBC 드라이버에서 사용 됩니다. 이 항목의 각 데이터 원본 및 해당 관련된 드라이버에 대 한 정보를 포함합니다. 데이터 원본에 연결할 수 있습니다, 전에 해당 연결 정보를 레지스트리에 추가 되어야 합니다.  
  
 추가 하 고 데이터 원본을 구성를 사용 하 여는 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)합니다. ODBC 관리자는 데이터 원본 연결 정보를 업데이트합니다. 데이터 소스를 추가 하면 ODBC 관리자 레지스트리 정보를 업데이트 합니다.  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 추가 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다.  
  
2.  ODBC 데이터 원본 관리자 대화 상자에서 추가 클릭 합니다. 새 데이터 소스 만들기 대화 상자가 나타납니다.  
  
3.  Oracle 용 Microsoft ODBC를 선택 하 고 마침을 클릭 합니다. Microsoft ODBC에 대 한 Oracle 설치 대화 상자가 나타납니다.  
  
4.  데이터 원본 이름 상자에 액세스 하려는 데이터 원본의 이름을 입력 합니다. 선택한 모든 이름을 수 있습니다.  
  
5.  설명 상자에 드라이버에 대 한 설명을 입력 합니다. 이 선택적 필드는 데이터 원본에 연결 하는 데이터베이스 드라이버를 설명 합니다. 선택한 모든 이름을 수 있습니다.  
  
6.  사용자 이름 상자에 데이터베이스 사용자 이름 (데이터베이스 사용자 ID)를 입력 합니다.  
  
7.  서버 입력란에 데이터베이스 별칭을 입력 하거나 연결 문자열에 액세스 하려면 Oracle 서버 엔진에 대 한 합니다.  
  
8.  이 데이터 원본을 추가 하려면 확인을 클릭 합니다.  
  
> [!NOTE]  
>  데이터 원본 대화 상자가 나타나고 ODBC 관리자 레지스트리 정보를 업데이트 합니다. 사용자 이름을 지정 하 고 연결 문자열 입력에 연결 하는 경우이 데이터 원본에 대 한 기본값이 연결 됩니다.  
  
1.  ODBC Driver for Oracle 설치에 대 한 자세한 정보가 옵션 만들기를 클릭 합니다.  
  
    -   **번역** -는 로드 된 데이터 변환기를 선택를 클릭 합니다. 기본값은 \<아니요 변환기 > 합니다.  
  
    -   **성능** — 카탈로그 함수 확인란의 The 포함 주의 드라이버에 대 한 설명 열을 반환 하는지 여부를 지정 된 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합입니다. Oracle에 대 한 ODBC 드라이버는이 값을 설정 하지 않은 경우 더 빠른 액세스를 제공 합니다.  
  
         드라이버 열 정보를 반환 하는지 여부를 지정 하는 SQL 열에 있는 동의어를 포함 합니다. **버퍼 크기** 인출 된 데이터를 받도록 할당 된 바이트 단위로 크기를 지정 합니다. 드라이버는 페치 한 인출 Oracle 서버에서 지정된 된 크기의 버퍼에 맞게 충분 한 행 반환 되도록 최적화 됩니다. 많은 데이터를 인출할 때 성능 향상을 위해 값이 클수록는 경향이 있습니다.  
  
    -   **사용자 지정** -The 적용 ODBC DayOfWeek 표준 확인란 (일요일 = 1; ODBC 지정된 주 일 형식으로 결과 집합을 따릅니다 있는지 여부를 지정 합니다. 토요일 = 7). 이 확인란의 선택을 취소 하는 경우에 로캘 특정 Oracle 값이 반환 됩니다.  
  
         SQLDescribeCol **항상 정밀도 대 한 값을 반환** 확인란 드라이버에 대 한 0이 아닌 값을 반환할지 여부를 지정 된 *cbColDef* 의 인수 **SQLDescribeCol**. 이 연결 문자열 특성 될 Oracle 정의 배율 없음 계산와 같은 숫자 열에만 적용 됩니다. 열과 열 또는 소수 자릿수가 없이 수로 정의 합니다. A **SQLDescribeCol** Oracle 해당 정보를 제공 하지 않는 전체 자릿수에 대 한 호출이 반환 130입니다. 이 확인란의 선택을 취소 하는 경우 드라이버는 이러한 유형의 열에 대 한 0를 대신 반환 합니다.  
  
2.  다른 데이터 원본을 추가 하려면 추가 클릭 하거나 종료 하려면 닫기를 클릭 합니다.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 수정 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다. 해당 하는 DSN 탭을 클릭 합니다.  
  
2.  Oracle 데이터 원본을 수정 하 고 구성을 클릭 한 다음를 선택 합니다. Microsoft ODBC에 대 한 Oracle 설치 대화 상자가 나타납니다.  
  
3.  적용 가능한 데이터 원본 필드를 수정 하 고 확인을 클릭 합니다.  
  
 이 대화 상자에서 정보를 수정 했으면 ODBC 관리자 레지스트리 정보를 업데이트 합니다.
