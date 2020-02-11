---
title: Oracle 용 ODBC 드라이버 구성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc163f53c9dc234702f6f74426eb65f57cec26b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096682"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버 구성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 Oracle에서 제공 하는 ODBC 드라이버를 사용 합니다.  
  
 데이터 환경을 파악 하 고 odbc [데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 대화 상자를 통해 또는 연결 문자열 매개 변수를 통해 데이터 원본 연결의 매개 변수를 올바르게 설정 하 여 ORACLE 용 ODBC 드라이버의 성능을 제어할 수 있습니다. 대화 상자에서는 대화 상자를 사용 하거나 연결 문자열을 사용 하 여 데이터 원본에 연결 하기 위한 다음과 같은 컨트롤을 제공 합니다.  
  
-   **사용자 DSN 탭** 컴퓨터에 로컬인 데이터 원본 이름을 나열 합니다.  
  
-   **시스템 DSN 탭** 시스템 데이터 원본을 추가 하거나 제거할 수 있습니다. 로컬 컴퓨터의 모든 사용자가 시스템 데이터 소스에 액세스할 수 있습니다.  
  
-   **파일 DSN 탭** 로컬 컴퓨터에서 파일 데이터 원본을 추가 하거나 제거할 수 있습니다. 파일 데이터 원본은 동일한 드라이버를 설치한 모든 사용자가 공유할 수 있습니다.  
  
-   **드라이버 탭** 설치 된 ODBC 드라이버를 나열 합니다.  
  
-   **추적 탭** Odbc 드라이버 관리자에서 ODBC 함수에 대 한 호출을 추적 하는 방법을 지정할 수 있습니다. 설치 된 각 ODBC 응용 프로그램에 대해 개별적으로 추적을 구성할 수 있습니다.  
  
-   **연결 풀링 탭** 설치 된 각 드라이버에 대 한 연결 옵션을 선택할 수 있습니다.  
  
-   **정보 탭** 설치 된 ODBC 구성 요소 파일을 나열 합니다.  
  
 데이터 원본을 추가한 후에는 **ODBC 데이터 원본 관리자** 대화 상자를 사용 하 여 데이터 원본에 대 한 액세스를 구성할 수 있습니다. 데이터 원본을 선택한 다음 탭 중 하나를 클릭 하 여 편집 하거나 정보를 검토 합니다.
