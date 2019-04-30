---
title: 레지스트리 항목 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de287802693adb18e39509fdc0e7577d05984949
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316833"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>레지스트리 항목(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 설치할 때 설치 프로그램이 Microsoft Visual FoxPro 드라이버 라는 새 키를 추가 하려면 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini 레지스트리 키에 시스템의 레지스트리를 업데이트 합니다. 다음 표에서 설명 하는 값은 해당 키 아래에 추가 됩니다.  
  
|값 이름|값 유형|값|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|드라이버|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|설치 프로그램|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
|SQLLevel|REG_SZ|"0"|  
  
 또한 설치 프로그램 "Visual FoxPro Files", 시스템의 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 키에 기본 Visual FoxPro 드라이버를 나타내는 키를 추가 합니다. 이 키에서 설치 프로그램은 다음 표에 설명 된 값을 추가 합니다.  
  
|값 이름|값 유형|값|  
|----------------|----------------|-----------|  
|드라이버|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
  
 ODBC 구성에 Visual FoxPro ODBC 데이터 소스를 추가할 때마다 새 키를 데이터 원본 이름에 추가 됩니다. 에 설정 된 값에 해당 하는 데이터 원본에 대 한 값을 **ODBC Visual FoxPro 설치** 대화 상자에서 다음 표에 나열 된 대로 합니다.  
  
|값 이름 (키워드)|값 유형|값|  
|----------------------------|----------------|-----------|  
|한 부씩 인쇄|REG_SQ|지원 되는 모든 데이터 정렬 순서|  
|Description|REG_SZ|데이터 원본의 사용자 설명|  
|드라이버||Vfpodbc.dll 파일 시스템 경로|  
|전용||Yes 또는 No|  
|BackgroundFetch||Yes 또는 No|  
|SourceDB|REG_SZ|경로입니다. Dbc입니다 파일|  
|SourceType|REG_SZ|"Dbc 입니다" 또는 "DBF"|  
  
 이 정보를 직접 액세스 하지 않아야 레지스트리의 모든 관리는 추가, 수정 또는 데이터 원본을 삭제 하는 경우 ODBC 관리자에 의해 처리 됩니다.  
  
 매개 변수로 이러한 키워드와 값의 일부를 사용 합니다 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 함수입니다.
