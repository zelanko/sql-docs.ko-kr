---
title: 설정을 사용하여 데이터 원본 추가 및 수정 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281413"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>설정을 사용하여 데이터 원본 추가 및 수정
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 데이터 원본은 네트워크 라이브러리, 서버, 데이터베이스 및 기타 특성을 포함할 수 있는 데이터 경로를 식별합니다.이 경우 데이터 원본은 Oracle 데이터베이스에 대한 경로입니다. 데이터 원본에 연결하기 위해 드라이버 관리자는 Windows 레지스트리에서 특정 연결 정보를 확인합니다.  
  
 ODBC 데이터 원본 관리자가 만든 레지스트리 항목은 ODBC 드라이버 관리자 및 ODBC 드라이버에서 사용됩니다. 이 항목에는 각 데이터 원본 및 관련 드라이버에 대한 정보가 포함되어 있습니다. 데이터 원본에 연결하려면 먼저 해당 연결 정보를 레지스트리에 추가해야 합니다.  
  
 데이터 원본을 추가하고 구성하려면 [ODBC 데이터 원본 관리자를](../../odbc/admin/odbc-data-source-administrator.md)사용합니다. ODBC 관리자는 데이터 원본 연결 정보를 업데이트합니다. 데이터 원본을 추가할 때 ODBC 관리자는 레지스트리 정보를 업데이트합니다.  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows용 데이터 원본을 추가하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다.  
  
2.  ODBC 데이터 원본 관리자 대화 상자에서 추가를 클릭합니다. Creat 새 데이터 원본 대화 상자가 나타납니다.  
  
3.  오라클의 경우 Microsoft ODBC를 선택한 다음 완료를 클릭합니다. 오라클 설치 대화 상자에 대 한 Microsoft ODBC 가 나타납니다.  
  
4.  데이터 원본 이름 상자에 액세스하려는 데이터 원본의 이름을 입력합니다. 선택한 모든 이름이 될 수 있습니다.  
  
5.  설명 상자에 드라이버에 대한 설명을 입력합니다. 이 선택적 필드는 데이터 원본이 연결하는 데이터베이스 드라이버를 설명합니다. 선택한 모든 이름이 될 수 있습니다.  
  
6.  사용자 이름 상자에 데이터베이스 사용자 이름(데이터베이스 사용자 ID)을 입력합니다.  
  
7.  서버 상자에서 데이터베이스 별칭을 입력하거나 액세스하려는 Oracle Server 엔진의 문자열을 연결합니다.  
  
8.  확인을 클릭하여 이 데이터 원본을 추가합니다.  
  
> [!NOTE]  
>  데이터 원본 대화 상자가 나타나고 ODBC 관리자가 레지스트리 정보를 업데이트합니다. 입력한 사용자 이름과 연결 문자열은 이 데이터 원본에 연결할 때 이 데이터 원본의 기본 연결 값이 됩니다.  
  
1.  클릭 옵션은 오라클 설정에 대한 ODBC 드라이버에 대한 더 많은 사양을 만듭니다.  
  
    -   **번역** - 선택을 클릭하여 로드된 데이터 번역기를 선택합니다. 기본값은 \<> 번역기 없음입니다.  
  
    -   **성능** - 카탈로그 함수에 REMARKS 포함 확인란에서 드라이버가 SQLColumns 결과 집합에 대한 비고 열을 반환할지 여부를 [지정합니다.](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 오라클의 ODBC 드라이버는 이 값을 설정하지 않을 때 더 빠른 액세스를 제공합니다.  
  
         SQL 열에 동의약 포함 확인란에는 드라이버가 열 정보를 반환할지 여부를 지정합니다. **버퍼 크기는** 가져온 데이터를 수신하기 위해 할당된 크기(바이트)를 지정합니다. 드라이버는 오라클 서버에서 가져온 하나의 가져오기가 지정된 크기의 버퍼를 채울 만큼 충분한 행을 반환하도록 페칭을 최적화합니다. 값이 클수록 많은 데이터를 가져올 때 성능이 향상되는 경향이 있습니다.  
  
    -   **사용자 지정** - ODBC DayOfWeek 표준 적용 확인란은 결과 집합이 ODBC 지정된 요일 형식(일요일 = 1)을 준수하는지 여부를 지정합니다. 토요일 = 7). 이 확인란을 선택 취소하면 로캘별 Oracle 값이 반환됩니다.  
  
         SQLDescribeCol은 항상 **드라이버가 SQLDescribeCol의** *cbColDef* 인수에 대해 0이 아닌 값을 반환할지 여부를 지정하는 정밀도 확인란에 대한 **값을 반환합니다.** 이 연결 문자열 특성은 정밀도 나 축척없이 NUMBER로 정의된 계산된 숫자 열 및 열과 같이 Oracle 정의 배율이 없는 열에만 적용됩니다. **SQLDescribeCol** 호출은 Oracle에서 해당 정보를 제공하지 않을 때 정밀도에 대해 130을 반환합니다. 이 확인란을 선택 취소하면 드라이버는 이러한 유형의 열에 대해 0을 반환합니다.  
  
2.  추가를 클릭하여 다른 데이터 원본을 추가하거나 종료할 닫기를 클릭합니다.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows용 데이터 원본을 수정하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다. 해당 DSN 탭을 클릭합니다.  
  
2.  수정할 Oracle 데이터 원본을 선택한 다음 구성을 클릭합니다. 오라클 설치 대화 상자에 대 한 Microsoft ODBC 가 나타납니다.  
  
3.  적용 가능한 데이터 원본 필드를 수정한 다음 확인을 클릭합니다.  
  
 이 대화 상자의 정보 수정을 완료하면 ODBC 관리자가 레지스트리 정보를 업데이트합니다.
