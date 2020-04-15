---
title: 오라클을 위한 ODBC 드라이버 구성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281373"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>Oracle용 ODBC 드라이버 구성
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 오라클에서 제공하는 ODBC 드라이버를 사용합니다.  
  
 데이터 환경을 알고 ODBC 데이터 원본 관리자 대화 상자 또는 연결 문자열 매개 변수를 통해 데이터 원본 연결의 매개 변수를 올바르게 설정하여 오라클의 [ODBC](../../odbc/admin/odbc-data-source-administrator.md) 드라이버 성능을 제어할 수 있습니다. 대화 상자는 대화 상자를 사용하거나 연결 문자열을 사용하여 데이터 원본에 연결하기 위한 다음 컨트롤을 제공합니다.  
  
-   **사용자 DSN 탭** 컴퓨터에 로컬인 데이터 원본 이름을 나열합니다.  
  
-   **시스템 DSN 탭** 시스템 데이터 원본을 추가하거나 제거할 수 있습니다. 시스템 데이터 원본은 로컬 컴퓨터의 모든 사용자가 액세스할 수 있습니다.  
  
-   **파일 DSN 탭** 로컬 컴퓨터에서 파일 데이터 원본을 추가하거나 제거할 수 있습니다. 동일한 드라이버가 설치된 모든 사용자가 파일 데이터 원본을 공유할 수 있습니다.  
  
-   **드라이버 탭** 설치된 ODBC 드라이버를 나열합니다.  
  
-   **추적 탭** ODBC 드라이버 관리자가 ODBC 함수에 대한 호출을 추적하는 방법을 지정할 수 있습니다. 설치된 각 ODBC 응용 프로그램에 대해 추적을 별도로 구성할 수 있습니다.  
  
-   **연결 풀링 탭** 설치된 각 드라이버에 대한 연결 옵션을 선택할 수 있습니다.  
  
-   **탭 소개** 설치된 ODBC 구성 요소 파일을 나열합니다.  
  
 데이터 원본을 추가한 후 **ODBC 데이터 원본 관리자** 대화 상자를 사용하여 데이터 원본에 대한 액세스를 구성할 수 있습니다. 데이터 원본을 선택한 다음 탭 중 하나를 클릭하여 정보를 편집하거나 검토합니다.
