---
title: 데스크톱 데이터베이스 드라이버 아키텍처 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288743"
---
# <a name="desktop-database-drivers-architecture"></a>데스크톱 데이터베이스 드라이버 아키텍처
이 드라이버는 마이크로 소프트 윈도우 95 이상, 또는 윈도우 NT 4.0 및 윈도우 2000에서 사용하도록 설계되었습니다. Windows 95 이상에서만 32비트 응용 프로그램이 지원됩니다. 16비트 및 32비트 응용 프로그램은 Windows NT 4.0 및 Windows 2000에서 지원됩니다.  
  
> [!NOTE]  
>  이러한 드라이버와 함께 사용할 ODBC 버전에 대한 자세한 내용은 *ODBC 프로그래머의 참조*및 과거 및 현재 릴리스 정보를 참조하십시오. 언급된 영역을 제외하고 이러한 드라이버는 *ODBC 프로그래머의 참조를 준수합니다.*  
  
 ODBC 데스크톱 데이터베이스 드라이버에는 마이크로소프트 액세스, dBASE, 마이크로소프트 엑셀, 역설 및 텍스트용 32비트 드라이버가 포함되어 있습니다. 16비트 드라이버는 포함되어 있지 않습니다. (마이크로소프트 폭스프로용 드라이버는 별도로 사용할 수 있습니다.)  
  
 Windows 95 이상에서 응용 프로그램/드라이버 아키텍처는 다음과 같은  
  
 ![응용 프로그램&#47;드라이버 아키텍처: 윈도우 95 이상](../../odbc/microsoft/media/odbcjetarch1.gif "ODBC젯아치1")  
  
 Windows 95에서 16비트 응용 프로그램에서 이러한 드라이버를 사용하는 것은 지원되지 않습니다.  
  
 Windows NT 4.0 및 Windows 2000의 응용 프로그램/드라이버 아키텍처는 다음과 같은 것입니다.  
  
 ![응용&#47;드라이버 아키텍처 : NT 4.0 및 윈도우 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 데스크톱 데이터베이스 드라이버는 2계층 드라이버입니다. 2계층 구성에서 드라이버는 쿼리구문 분석, 유효성 검사, 최적화 및 실행 프로세스를 수행하지 않습니다. 대신 Microsoft Jet에서 이러한 작업을 수행합니다. ODBC API 호출을 처리하고 SQL 엔진역할을 합니다. 마이크로 소프트 제트는 드라이버의 필수적인, 분리 할 수없는 부분이되었다 : 그것은 드라이버와 함께 제공및 드라이버와 함께 상주, 컴퓨터에 다른 응용 프로그램이 그것을 사용하지 않는 경우에도.  
  
 데스크톱 데이터베이스 드라이버는 ODBC 드라이버 [관리자가](../../odbc/reference/the-driver-manager.md) 6가지 방법으로 사용하는 6개의 서로 다른 드라이버 또는 더 정확하게는 하나의 드라이버 파일(Odbcjt32.dll)으로 구성됩니다. 데이터 원본에 대한 레지스트리 항목의 DRIVERID 플래그는 드라이버 관리자가 사용하는 Odbcjt32.dll의 드라이버를 결정합니다. 응용 프로그램은 **SQLDriverConnect**에 대한 호출에 포함된 연결 문자열에서 이 플래그를 전달합니다. 기본적으로 플래그는 Microsoft Access 드라이버의 ID입니다.  
  
 드라이버 설정 파일은 설정 시 DRIVERID 플래그를 변경합니다. Microsoft Access 드라이버를 제외한 모든 드라이버에는 연결된 설정 DLL이 있습니다. 데이터 원본에 대한 [Microsoft ODBC 데이터 원본 관리자의](../../odbc/admin/odbc-data-source-administrator.md) **설정을** 클릭하면 ODBC 설치 관리자 DLL(Odbcinst.dll)이 설치 DLL을 로드합니다. 설치 DLL은 ODBC 설치 프로그램 함수 **SQLConfigDataSource를**내보전합니다. 창 핸들이 **SQLConfigDataSource에**전달되는 경우 이 함수는 설치 창을 표시하고 사용자 인터페이스에서 선택한 드라이버에 따라 DRIVERID 플래그를 변경합니다.  
  
 파일이 프로그래밍 방식으로 만들어지면 NULL 창 핸들이 **SQLConfigDataSource에**전달되고 함수는 함수 호출의 *lpszDriver* 인수에 따라 DRIVERID 플래그를 변경하여 동적으로 데이터 원본을 만듭니다.  
  
 Odbcjt32.dll은 마이크로소프트 제트 API 위에 ODBC 기능을 구현합니다. 그러나 ODBC와 Microsoft Jet 기능 간에는 직접 매핑이 없습니다. 커서 모델 및 SQL 매핑과 같은 많은 요인이 함수의 직접적인 상관 관계를 방지합니다.  
  
 ODBC 드라이버는 Microsoft 제트 엔진과 ODBC 드라이버 관리자 사이에 있습니다. 응용 프로그램에서 호출하는 일부 ODBC 함수는 드라이버 관리자에서 처리하며 드라이버에 전달되지 않습니다. 이러한 함수의 경우 드라이버 관리자에 직접 연결되지 않으므로 Microsoft Jet에서 함수 호출을 볼 수 없습니다.
