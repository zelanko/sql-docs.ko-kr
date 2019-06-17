---
title: ODBC Jet SQLConfigDataSource (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbad3b1e6dda82a9f9fc584683e53f8e2a109cca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63233596"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 합니다 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 또는 데이터 원본 삭제 동적으로 다음과 같은 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|DBQ|Microsoft Excel 드라이버의 Microsoft Excel 5.0 또는 이후 파일에 액세스할 때 통합 문서 파일의 이름입니다.<br /><br /> 동일한 옵션을 설정 **데이터베이스** 설정 대화 상자에서.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.<br /><br /> 동일한 옵션을 설정 **디렉터리 선택** 또는 **통합 문서 선택** 설정 대화 상자에서.|  
|DESCRIPTION|데이터 원본에 있는 데이터의 설명입니다.<br /><br /> 동일한 옵션을 설정 **설명을** 설정 대화 상자에서.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버에 대 한 정수 ID입니다.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|파일 형식, 예를 들어 Excel 3.0, Excel 4.0, 5.0 Excel, Excel 7.0, Excel 97, Excel 2000 또는 Excel 2003입니다.|  
|FIRSTROWHASNAMES|범위의 첫 번째 행의 셀 여부 (1) 테이블의 열 이름을 포함 하는지 여부를 나타냅니다 (0).|  
|MAXSCANROWS|기존 데이터를 기반으로 하는 열의 데이터 형식을 설정 하는 경우 검색할 행의 수입니다.<br /><br /> 검색할 행에 대해 1에서 16 사이의 숫자로 입력할 수 있습니다. 기본값은 8입니다. 0으로 설정 하는 경우 모든 행 검사 됩니다. (제한 벗어나는 숫자로 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 **검색할 행** 설정 대화 상자에서.|  
|READONLY|읽기 전용 파일을 확인. 읽기 전용 파일을 만들기 위해 FALSE입니다.<br /><br /> 동일한 옵션을 설정 **읽기 전용** 설정 대화 상자에서.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드의 수입니다. Microsoft Access 드라이버의 경우이 값을 3으로 기본적으로 사용 되지만 변경할 수 있습니다. DBASE, MicrosoftExceldriver이이 값은 3을 변경할 수 없습니다.<br /><br /> 동일한 옵션을 설정 **스레드** 설정 대화 상자에서.|
