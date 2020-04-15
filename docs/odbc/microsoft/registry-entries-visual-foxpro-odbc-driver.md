---
title: 레지스트리 항목 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304840"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>레지스트리 항목(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 설치하면 설치 프로그램이 레지스트리 키 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini에서 시스템의 레지스트리를 업데이트하여 Microsoft Visual FoxPro 드라이버라는 새 키를 추가합니다. 이 키 아래에다음 표에 설명된 값이 추가됩니다.  
  
|값 이름|값 형식|값|  
|----------------|----------------|-----------|  
|API 레벨|REG_SZ|"1"|  
|커넥트 기능|REG_SZ|"YYN"|  
|드라이버|REG_SZ|vfpodbc.dll 파일에 대한 시스템 경로|  
|DriverODBCVer|REG_SZ|"02.50"|  
|파일 익스트른|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|파일 사용|REG_SZ|"1"|  
|설치 프로그램|REG_SZ|vfpodbc.dll 파일에 대한 시스템 경로|  
|SQL수준|REG_SZ|"0"|  
  
 또한 설치 프로그램은 기본 Visual FoxPro 드라이버를 나타내는 키 "Visual FoxPro 파일"을 시스템의 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini 키에 추가합니다. 이 키 아래에 설치 프로그램은 다음 표에 설명된 값을 추가합니다.  
  
|값 이름|값 형식|값|  
|----------------|----------------|-----------|  
|드라이버|REG_SZ|vfpodbc.dll 파일에 대한 시스템 경로|  
  
 ODBC 구성에 Visual FoxPro ODBC 데이터 원본을 추가할 때마다 해당 데이터 원본 이름에 대해 새 키가 추가됩니다. 데이터 원본의 값은 다음 표에 나열된 **ODBC Visual FoxPro 설치** 대화 상자에 설정한 값과 일치합니다.  
  
|값 이름(키워드)|값 형식|값|  
|----------------------------|----------------|-----------|  
|한 부씩 인쇄|REG_SQ|지원되는 모든 정렬 순서|  
|설명|REG_SZ|데이터 원본에 대한 사용자 설명|  
|드라이버||vfpodbc.dll 파일에 대한 시스템 경로|  
|단독||Yes 또는 No|  
|백그라운드 페치||Yes 또는 No|  
|SourceDB|REG_SZ|로의 경로 DBC 파일|  
|SourceType|REG_SZ|"DBC" 또는 "DBF"|  
  
 이 정보에 직접 액세스해서는 안 됩니다. 레지스트리의 모든 관리는 데이터 원본을 추가, 수정 또는 삭제할 때 ODBC 관리자가 처리합니다.  
  
 이러한 키워드 와 값 중 일부를 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) ODBC API 함수의 매개 변수로 사용할 수 있습니다.
