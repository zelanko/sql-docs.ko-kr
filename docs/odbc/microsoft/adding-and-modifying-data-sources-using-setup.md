---
title: 설치 프로그램을 사용 하 여 원본 데이터 추가 및 수정 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 621d10c3c602b2f406461a24e53b2302e45835eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901400"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>설정을 사용하여 데이터 원본 추가 및 수정
> [!IMPORTANT]  
>  이 기능은 Windows의 이후 버전에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신, Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 네트워크 라이브러리, 서버, 데이터베이스 및 기타 특성을 포함할 수 있는 데이터에 대 한 경로 식별 하는 데이터 원본-이 경우 데이터 원본이 Oracle 데이터베이스에 대 한 경로입니다. 데이터 원본에 연결 하려면 드라이버 관리자는 특정 연결 정보에 대 한 Windows 레지스트리를 확인 합니다.  
  
 ODBC 데이터 원본 관리자가 만든 레지스트리 항목은 ODBC 드라이버 관리자 및 ODBC 드라이버에서 사용 됩니다. 이 항목의 각 데이터 원본 및 해당 관련된 드라이버에 대 한 정보를 포함합니다. 데이터 원본에 연결할 수 전에 해당 연결 정보를 레지스트리에 추가 되어야 합니다.  
  
 추가한 데이터 원본을 구성 하려면 사용 합니다 [ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md)합니다. ODBC 관리자는 데이터 원본 연결 정보를 업데이트합니다. 데이터 소스를 추가 하면 ODBC 관리자 레지스트리 정보를 업데이트 합니다.  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 추가 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다.  
  
2.  ODBC 데이터 원본 관리자 대화 상자에서 추가 클릭 합니다. 새 데이터 소스 만들기 대화 상자가 나타납니다.  
  
3.  Microsoft ODBC for Oracle 선택한 다음 마침을 클릭 합니다. Microsoft ODBC for Oracle 설치 대화 상자가 나타납니다.  
  
4.  데이터 원본 이름 상자에 액세스 하려는 데이터 원본의 이름을 입력 합니다. 사용자가 선택한 모든 이름이 수 있습니다.  
  
5.  설명 상자에 드라이버에 대 한 설명을 입력 합니다. 이 선택적 필드는 데이터 원본에 연결 하는 데이터베이스 드라이버를 설명 합니다. 사용자가 선택한 모든 이름이 수 있습니다.  
  
6.  사용자 이름 상자에 데이터베이스 사용자 이름 (데이터베이스 사용자 ID)를 입력 합니다.  
  
7.  서버 상자에서 데이터베이스 별칭을 입력 하거나 액세스 하려면 Oracle 서버 엔진에 대 한 문자열을 연결 합니다.  
  
8.  이 데이터 원본을 추가 하려면 확인을 클릭 합니다.  
  
> [!NOTE]  
>  데이터 원본 대화 상자가 나타나고 ODBC 관리자에 레지스트리 정보를 업데이트 합니다. 사용자 이름을 지정 하 고 연결 문자열 입력에 연결할 때이 데이터 원본에 대 한 기본값이 연결 됩니다.  
  
1.  ODBC Driver for Oracle 설치에 대 한 자세한 정보가 옵션 확인을 클릭 합니다.  
  
    -   **번역** -로드 한 데이터 변환기를 선택할 수 선택을 클릭 합니다. 기본값은 \<아니요 Translator >.  
  
    -   **성능** -확인란 카탈로그 함수는 포함 주의 드라이버에 대 한 설명 열을 반환 하는지 여부를 지정 합니다 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md) 결과 집합입니다. Oracle 용 ODBC 드라이버는이 값이 설정 되지 않은 빠른 액세스를 제공 합니다.  
  
         SQL 열 확인란에 포함할 동의어 드라이버 열 정보를 반환 하는지 여부를 지정 합니다. **버퍼 크기** 인출된 데이터 수신에 할당 된 바이트의 크기를 지정 합니다. 드라이버를 가져오는 Oracle 서버 로부터의 페치에서 하나 지정된 된 크기의 버퍼에 맞게 충분 한 행 반환 되도록 최적화 합니다. 많은 양의 데이터를 인출할 때 성능을 향상 시키기 위해 값이 클수록 경향이 있습니다.  
  
    -   **사용자 지정** -적용 ODBC DayOfWeek 표준 확인란 결과 집합 (일요일 = 1; ODBC 지정된-요일 형식을 준수가 있는지 여부를 지정 합니다. 토요일 = 7). 이 확인란의 선택을 취소 하면 로캘별 Oracle 값이 반환 됩니다.  
  
         SQLDescribeCol **항상 전체 자릿수 값이 반환** 확인란 드라이버에 대 한 0이 아닌 값을 반환할지 여부를 지정 합니다 *cbColDef* 인수의 **SQLDescribeCol**. 이 연결 문자열 특성 될 Oracle 정의한 비율이 없는 계산 같은 숫자 열에만 적용 됩니다. 열과 열 전체 자릿수 또는 확장 없이 수로 정의 합니다. A **SQLDescribeCol** Oracle 해당 정보를 제공 하지 않는 경우 전체 자릿수에 대 한 호출이 반환 130입니다. 이 확인란의 선택을 취소 하는 경우 드라이버는 이러한 유형의 열에 대 한 0를 대신 반환 됩니다.  
  
2.  다른 데이터 원본을 추가 하려면 추가 클릭 하거나 종료 하려면 닫기를 클릭 합니다.  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows에 대 한 데이터 원본을 수정 하려면  
  
1.  ODBC 데이터 원본 관리자를 엽니다. 해당 하는 DSN 탭을 클릭 합니다.  
  
2.  수정 하 고 누른 다음 구성 하려는 Oracle 데이터 원본을 선택 합니다. Microsoft ODBC for Oracle 설치 대화 상자가 나타납니다.  
  
3.  해당 데이터 원본 필드를 수정 하 고 확인을 클릭 합니다.  
  
 이 대화 상자에서 정보를 수정 했으면 ODBC 관리자에 레지스트리 정보를 업데이트 합니다.
