---
title: 레지스트리 항목 (ODBC 드라이버 Visual FoxPro) | Microsoft Docs
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
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0044d938baf62391a21afd273fd7a5b21c25a969
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>레지스트리 항목 (Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 설치할 때 설치 프로그램이 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini Microsoft Visual FoxPro 드라이버 라는 새 키를 추가 하려면 레지스트리 키에서 시스템의 레지스트리를 업데이트 합니다. 해당 키 아래에 다음 표에 설명 된 값이 추가 됩니다.  
  
|값 이름|값 유형|Value|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|드라이버|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|설치 프로그램|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
|SQLLevel|REG_SZ|"0"|  
  
 설치 프로그램은 또한 Visual FoxPro 파일 "" 시스템의 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 키에는 기본 Visual FoxPro 드라이버를 나타내는 키를 추가 합니다. 이 키에서 설치 프로그램은 다음 표에 설명 된 값을 추가 합니다.  
  
|값 이름|값 유형|Value|  
|----------------|----------------|-----------|  
|드라이버|REG_SZ|Vfpodbc.dll 파일 시스템 경로|  
  
 ODBC 구성으로 Visual FoxPro ODBC 데이터 소스를 추가할 때마다 새 키에 대 한 데이터 원본 이름 추가 됩니다. 에 설정 된 값에 해당 하는 데이터 원본에 대 한 값은 **ODBC Visual FoxPro 설정** 대화 상자에서 다음 표에 나열 된 합니다.  
  
|값 이름 (키워드)|값 유형|Value|  
|----------------------------|----------------|-----------|  
|한 부씩 인쇄|REG_SQ|지원 되는 모든 데이터 정렬 순서|  
|Description|REG_SZ|데이터 원본에 대 한 사용자 설명|  
|드라이버||Vfpodbc.dll 파일 시스템 경로|  
|단독||Yes 또는 No|  
|BackgroundFetch||Yes 또는 No|  
|SourceDB|REG_SZ|경로입니다. Dbc입니다 파일|  
|SourceType|REG_SZ|"Dbc 입니다" 또는 "DBF"|  
  
 이 정보를 직접 액세스 하지 않아야 모든 관리는 레지스트리의 추가, 수정 또는 데이터 원본을 삭제 하는 경우 ODBC 관리자에 의해 처리 됩니다.  
  
 이러한 키워드와 값 중 일부에 매개 변수로 사용할 수 있습니다는 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 함수입니다.
