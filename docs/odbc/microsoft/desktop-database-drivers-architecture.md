---
title: "데스크톱 데이터베이스 드라이버 아키텍처 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b85711437c50ccc246ad1af1432d9475d1cfc3d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="desktop-database-drivers-architecture"></a>데스크톱 데이터베이스 드라이버 아키텍처
이러한 드라이버는 사용 하 여 Microsoft Windows 95 이상 또는 Windows NT 4.0 및 Windows 2000 위한 것입니다. Windows 95 이상; 32 비트 응용 프로그램만 지원 됩니다. 16 비트 및 32 비트 응용 프로그램은 Windows NT 4.0 및 Windows 2000에서 지원 됩니다.  
  
> [!NOTE]  
>  이들이 드라이버를 함께 사용 되는 ODBC의 버전에 대 한 정보에 대 한 참조는 *ODBC 프로그래머 참조*, 및 과거 및 현재 릴리스 정보입니다. 명시 된 영역을 제외 하 고 이들이 드라이버를 준수는 *ODBC Programmer's Reference*합니다.  
  
 ODBC 데스크톱 데이터베이스 드라이버는 Microsoft Access, dBASE, Microsoft Excel, Paradox 및 텍스트에 대 한 32 비트 드라이버를 포함 합니다. 아니요-16 비트 드라이버가 포함 됩니다. (Microsoft FoxPro에 대 한 드라이버는 별도로 제공 됩니다.)  
  
 다음은 Windows 95 이상 응용 프로그램/드라이버 아키텍처가입니다.  
  
 ![응용 프로그램 &#47; 드라이버 아키텍처: Windows 95 이상](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Windows 95에서 16 비트 응용 프로그램에서 이들이 드라이버를 사용 하는 지원 되지 않습니다.  
  
 다음은 Windows NT 4.0 및 Windows 2000에서 응용 프로그램/드라이버 아키텍처가입니다.  
  
 ![응용 프로그램 &#47; 드라이버 아키텍처: NT 4.0 및 Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 데스크톱 데이터베이스 드라이버는 2 계층 드라이버. 2 계층 구성에서 드라이버는 구문 분석, 유효성 검사, 최적화 및 쿼리를 실행 하는 과정을 수행 하지 않습니다. 대신, Microsoft Jet는 이러한 작업을 수행합니다. ODBC API 호출을 처리 하 고 SQL 엔진으로 작동 합니다. Microsoft Jet 드라이버에서 정수 계열, 분리 불가능 부분이 되었습니다: 드라이버와 함께 제공 하 고 컴퓨터에서 다른 응용 프로그램에서 사용 하는 경우에 된 드라이버와 함께 상주 합니다.  
  
 데스크톱 데이터베이스 드라이버는 6 명의 다른 드라이버 구성-보다 정확 하 게 하나의 드라이버 파일 (Odbcjt32.dll) 또는 하는 ODBC [드라이버 관리자](../../odbc/reference/the-driver-manager.md) 6 가지 다른 방법으로 사용 합니다. 데이터 원본에 대 한 레지스트리 항목에 DRIVERID 플래그 Odbcjt32.dll에서 드라이버는 드라이버 관리자는 사용 결정 합니다. 응용 프로그램에 대 한 호출에 포함 된 연결 문자열에서이 플래그를 전달 **SQLDriverConnect**합니다. 기본적으로 플래그에는 Microsoft Access 드라이버의 ID입니다.  
  
 드라이버 설치 파일 설치 시 DRIVERID 플래그를 변경 합니다. Microsoft Access 드라이버를 제외한 모든 드라이버 DLL 연결된 설정 된 경우 클릭할 때 **설치** 에 [Microsoft ODBC 데이터 원본 관리자](../../odbc/admin/odbc-data-source-administrator.md) ODBC 설치 DLL (Odbcinst.dll) 데이터 원본에 대 한 설치 DLL을 로드 합니다. 설치 DLL ODBC 설치 관리자 함수를 내보내는 **SQLConfigDataSource**합니다. 창 핸들에 전달 되 면 **SQLConfigDataSource**,이 함수는 설치 프로그램 창을 표시 하 고 사용자 인터페이스에서 선택한 드라이버에 따라 DRIVERID 플래그를 변경 합니다.  
  
 파일을 만들 프로그래밍 방식으로, NULL 창 핸들에 전달 됩니다 **SQLConfigDataSource**, 함수는 데이터 원본을 만듭니다 동적으로 DRIVERID 플래그에 따라 변경 하 고는 *lpszDriver*함수 호출의 인수입니다.  
  
 Odbcjt32.dll은 Microsoft Jet API를 기반으로 ODBC 함수를 구현합니다. 그러나 ODBC 및 Microsoft Jet 함수 간의 직접 매핑되지가 않습니다. 커서 모델 및 SQL 매핑을 등 많은 요인 함수는 직접적인 상관 관계가 방지합니다.  
  
 ODBC 드라이버는 ODBC 드라이버 관리자와 Microsoft Jet 엔진 간의 상주합니다. 응용 프로그램에서 호출 하는 일부 ODBC 함수 드라이버 관리자에서 처리 및 드라이버에 전달 되지 않습니다. 이러한 함수에 대 한 Microsoft Jet는 함수 호출에 직접 연결 드라이버 관리자에 없기 때문에 표시 되지 않습니다.
