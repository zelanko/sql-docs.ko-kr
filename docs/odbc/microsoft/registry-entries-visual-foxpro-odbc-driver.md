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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304840"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>레지스트리 항목(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 설치 하는 경우 설치 프로그램은 \SOFTWARE\ODBC\ODBCInst.ini HKEY_LOCAL_MACHINE 레지스트리 키에서 시스템의 레지스트리를 업데이트 하 여 Microsoft Visual FoxPro 드라이버 라는 새 키를 추가 합니다. 해당 키 아래에 다음 표에 설명 된 값이 추가 됩니다.  
  
|값 이름|값 형식|값|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|드라이버|REG_SZ|Vfpodbc 파일에 대 한 시스템 경로|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"* .dbf,\*cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|설치 프로그램|REG_SZ|Vfpodbc 파일에 대 한 시스템 경로|  
|SQLLevel|REG_SZ|"0"|  
  
 또한 설치 프로그램에서는 기본 Visual FoxPro 드라이버를 나타내는 "Visual FoxPro 파일" 키를 시스템의 HKEY_CURRENT_USER \SOFTWARE\ODBC\Odbc.ini 키에 추가 합니다. 이 키 아래에 설치 프로그램은 다음 표에 설명 된 값을 추가 합니다.  
  
|값 이름|값 형식|값|  
|----------------|----------------|-----------|  
|드라이버|REG_SZ|Vfpodbc 파일에 대 한 시스템 경로|  
  
 ODBC 구성에 Visual FoxPro ODBC 데이터 원본을 추가할 때마다 해당 데이터 원본 이름에 대해 새 키가 추가 됩니다. 데이터 원본에 대 한 값은 다음 표에 나열 된 **ODBC Visual FoxPro** 설정 대화 상자에서 설정한 값에 해당 합니다.  
  
|값 이름 (키워드)|값 형식|값|  
|----------------------------|----------------|-----------|  
|한 부씩 인쇄|REG_SQ|모든 지원 되는 데이터 정렬 순서|  
|설명|REG_SZ|데이터 원본에 대 한 사용자 설명|  
|드라이버||Vfpodbc 파일에 대 한 시스템 경로|  
|단독||Yes 또는 No|  
|BackgroundFetch||Yes 또는 No|  
|SourceDB|REG_SZ|의 경로입니다. DBC 파일|  
|SourceType|REG_SZ|"DBC" 또는 "DBF"|  
  
 이 정보는 직접 액세스 하면 안 됩니다. 레지스트리 관리는 데이터 원본을 추가, 수정 또는 삭제할 때 ODBC 관리자에 의해 처리 됩니다.  
  
 이러한 키워드 및 값 중 일부를 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 함수에서 매개 변수로 사용할 수 있습니다.
