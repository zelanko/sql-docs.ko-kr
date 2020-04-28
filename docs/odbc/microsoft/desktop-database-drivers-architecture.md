---
title: 데스크톱 데이터베이스 드라이버 아키텍처 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288743"
---
# <a name="desktop-database-drivers-architecture"></a>데스크톱 데이터베이스 드라이버 아키텍처
이러한 드라이버는 Microsoft Windows 95 이상 또는 Windows NT 4.0 및 Windows 2000에서 사용 하도록 설계 되었습니다. 32 비트 응용 프로그램만 Windows 95 이상에서 지원 됩니다. Windows NT 4.0 및 Windows 2000에서 16 비트 및 32 비트 응용 프로그램이 지원 됩니다.  
  
> [!NOTE]  
>  이러한 드라이버에 사용할 ODBC 버전에 대 한 자세한 내용은 *Odbc 프로그래머 참조*및 과거 및 현재 릴리스 정보를 참조 하세요. 표시 된 영역을 제외 하 고 이러한 드라이버는 *ODBC 프로그래머 참조*를 따릅니다.  
  
 ODBC 데스크톱 데이터베이스 드라이버는 Microsoft Access, dBASE, Microsoft Excel, Paradox 및 텍스트에 대 한 32 비트 드라이버를 포함 합니다. 16 비트 드라이버가 포함 되지 않습니다. Microsoft FoxPro 용 드라이버는 별도로 제공 됩니다.  
  
 Windows 95 이상에서 응용 프로그램/드라이버 아키텍처는 다음과 같습니다.  
  
 ![앱&#47;드라이버 아키텍처: Windows 95 이상](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Windows 95의 16 비트 응용 프로그램에서 이러한 드라이버를 사용 하는 것은 지원 되지 않습니다.  
  
 Windows NT 4.0 및 Windows 2000의 응용 프로그램/드라이버 아키텍처는 다음과 같습니다.  
  
 ![앱&#47;드라이버 아키텍처: NT 4.0 및 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 데스크톱 데이터베이스 드라이버는 2 계층 드라이버입니다. 2 계층 구성에서는 드라이버가 쿼리를 구문 분석 하 고, 유효성을 검사 하 고, 최적화 하 고, 실행 하는 프로세스를 수행 하지 않습니다. 대신 Microsoft Jet에서 이러한 작업을 수행 합니다. ODBC API 호출을 처리 하 고 SQL 엔진 역할을 합니다. Microsoft Jet는 드라이버와 함께 제공 되며, 컴퓨터의 다른 응용 프로그램에서 사용 하지 않는 경우에도 드라이버와 함께 제공 되며 드라이버와 함께 제공 됩니다.  
  
 데스크톱 데이터베이스 드라이버는 ODBC [드라이버 관리자](../../odbc/reference/the-driver-manager.md) 가 6 가지 방법으로 사용 하는 여섯 가지 드라이버 파일 (Odbcjt32) 또는 더 정확 하 게 하나의 드라이버 파일 ()로 구성 됩니다. 데이터 원본에 대 한 레지스트리 항목의 DRIVERID 플래그는 드라이버 관리자에서 사용 하는 Odbcjt32의 드라이버를 결정 합니다. 응용 프로그램은 **SQLDriverConnect**에 대 한 호출에 포함 된 연결 문자열에이 플래그를 전달 합니다. 기본적으로 플래그는 Microsoft Access 드라이버의 ID입니다.  
  
 드라이버 설치 파일은 설치 시 DRIVERID 플래그를 변경 합니다. Microsoft Access 드라이버를 제외한 모든 드라이버에는 연결 된 설치 DLL이 있습니다. 데이터 원본에 대 한 [MICROSOFT Odbc 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) 에서 **설치** 를 클릭 하면 ODBC 설치 관리자 dll (ODBCINST.INI)에서 설치 dll을 로드 합니다. 설치 DLL은 ODBC 설치 관리자 함수 **SQLConfigDataSource**을 내보냅니다. 창 핸들이 **SQLConfigDataSource**에 전달 되 면이 함수는 설정 창을 표시 하 고 사용자 인터페이스에서 선택한 드라이버에 따라 driverid 플래그를 변경 합니다.  
  
 프로그래밍 방식으로 파일을 만들면 NULL 창 핸들이 **SQLConfigDataSource**로 전달 되 고 함수는 함수 호출의 *lpszDriver* 인수에 따라 driverid 플래그를 변경 하 여 데이터 소스를 동적으로 만듭니다.  
  
 Odbcjt32는 Microsoft Jet API 위에 있는 ODBC 함수를 구현 합니다. 그러나 ODBC와 Microsoft Jet 함수 사이에는 직접적인 매핑이 없습니다. 커서 모델 및 SQL 매핑과 같은 많은 요소는 함수에 대 한 직접적인 상관 관계를 방지 합니다.  
  
 ODBC 드라이버는 Microsoft Jet 엔진과 ODBC 드라이버 관리자 사이에 상주 합니다. 응용 프로그램에서 호출 하는 일부 ODBC 함수는 드라이버 관리자에 의해 처리 되며 드라이버에 전달 되지 않습니다. 이러한 함수의 경우 Microsoft Jet는 드라이버 관리자에 대 한 직접 연결이 없기 때문에 함수 호출을 볼 수 없습니다.
