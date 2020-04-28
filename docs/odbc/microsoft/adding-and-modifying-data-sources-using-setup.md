---
title: 설치 프로그램을 사용 하 여 데이터 원본 추가 및 수정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae76abc902e4687e5d9891871d7d5d60598b3abc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281413"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>설정을 사용하여 데이터 원본 추가 및 수정
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 데이터 원본은 네트워크 라이브러리, 서버, 데이터베이스 및 기타 특성을 포함할 수 있는 데이터의 경로를 식별 합니다 .이 경우 데이터 원본은 Oracle 데이터베이스에 대 한 경로입니다. 데이터 원본에 연결 하기 위해 드라이버 관리자는 Windows 레지스트리에서 특정 연결 정보를 확인 합니다.  
  
 Odbc 데이터 원본 관리자가 만든 레지스트리 항목은 ODBC 드라이버 관리자 및 ODBC 드라이버에서 사용 됩니다. 이 항목에는 각 데이터 원본 및 관련 드라이버에 대 한 정보가 포함 되어 있습니다. 데이터 원본에 연결 하려면 먼저 해당 연결 정보를 레지스트리에 추가 해야 합니다.  
  
 데이터 원본을 추가 하 고 구성 하려면 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)를 사용 합니다. ODBC 관리자는 데이터 원본 연결 정보를 업데이트 합니다. 데이터 원본을 추가 하면 ODBC 관리자가 레지스트리 정보를 업데이트 합니다.  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 추가 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다.  
  
2.  ODBC 데이터 원본 관리자 대화 상자에서 추가를 클릭 합니다. 새 데이터 소스 만들기 대화 상자가 나타납니다.  
  
3.  Oracle 용 Microsoft ODBC를 선택 하 고 마침을 클릭 합니다. Oracle 용 Microsoft ODBC 설치 대화 상자가 나타납니다.  
  
4.  데이터 원본 이름 상자에 액세스 하려는 데이터 원본의 이름을 입력 합니다. 사용자가 선택한 모든 이름일 수 있습니다.  
  
5.  설명 상자에 드라이버에 대 한 설명을 입력 합니다. 이 선택적 필드는 데이터 원본이 연결 되는 데이터베이스 드라이버를 설명 합니다. 사용자가 선택한 모든 이름일 수 있습니다.  
  
6.  사용자 이름 상자에 데이터베이스 사용자 이름 (데이터베이스 사용자 ID)을 입력 합니다.  
  
7.  서버 상자에 액세스 하려는 Oracle 서버 엔진에 대 한 데이터베이스 별칭 또는 연결 문자열을 입력 합니다.  
  
8.  확인을 클릭 하 여이 데이터 원본을 추가 합니다.  
  
> [!NOTE]  
>  데이터 원본 대화 상자가 나타나고 ODBC 관리자가 레지스트리 정보를 업데이트 합니다. 입력 한 사용자 이름 및 연결 문자열은이 데이터 원본에 연결할 때이 데이터 원본에 대 한 기본 연결 값이 됩니다.  
  
1.  Oracle 용 ODBC 드라이버 설치에 대 한 추가 사양 만들기 옵션을 클릭 합니다.  
  
    -   **번역** -로드 된 데이터 변환기를 선택 하려면 선택을 클릭 합니다. 기본값은 변환기 \<> 없습니다.  
  
    -   **성능** -카탈로그 함수에 설명 포함 확인란은 드라이버가 [sqlcolumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합에 대 한 설명 열을 반환 하는지 여부를 지정 합니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 경우 더 빠른 액세스를 제공 합니다.  
  
         SQL 열에 동의어 포함 확인란은 드라이버가 열 정보를 반환 하는지 여부를 지정 합니다. **버퍼 크기** 는 인출 된 데이터를 받도록 할당 된 크기 (바이트)를 지정 합니다. 드라이버는 가져오기를 최적화 하 여 Oracle 서버에서 하나의 가져오기가 지정 된 크기의 버퍼를 채우도록 충분 한 행을 반환 합니다. 값이 클수록 많은 데이터를 가져올 때 성능이 향상 됩니다.  
  
    -   **사용자 지정** -Odbc DayOfWeek 표준 적용 확인란은 결과 집합이 odbc 지정 된 요일 형식 (일요일 = 1;)을 따르는지 여부를 지정 합니다. 토요일 = 7). 이 확인란의 선택을 취소 하면 로캘별 Oracle 값이 반환 됩니다.  
  
         SQLDescribeCol는 **항상 전체 자릿수에 대 한 값을 반환** 합니다. 확인란은 드라이버가 **SQLDescribeCol**의 *cbcoldef* 인수에 대해 0이 아닌 값을 반환 해야 하는지 여부를 지정 합니다. 이 연결 문자열 특성은 계산 된 숫자 열 및 전체 자릿수가 나 소수 자릿수가 없는 숫자로 정의 된 열과 같이 Oracle에서 정의한 소수 자릿수가 없는 열에만 적용 됩니다. **SQLDescribeCol** 호출은 Oracle에서 해당 정보를 제공 하지 않을 때 전체 자릿수에 대해 130을 반환 합니다. 이 확인란의 선택을 취소 하면 드라이버에서 이러한 열 형식에 대해 0을 반환 합니다.  
  
2.  추가를 클릭 하 여 다른 데이터 원본을 추가 하거나 닫기를 클릭 하 여 종료 합니다.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 수정 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다. 적절 한 DSN 탭을 클릭 합니다.  
  
2.  수정 하려는 Oracle 데이터 원본을 선택 하 고 구성을 클릭 합니다. Oracle 용 Microsoft ODBC 설치 대화 상자가 나타납니다.  
  
3.  적용 가능한 데이터 원본 필드를 수정한 다음 확인을 클릭 합니다.  
  
 이 대화 상자의 정보를 수정한 후에는 ODBC 관리자가 레지스트리 정보를 업데이트 합니다.
