---
title: "ODBC Jet SQLConfigDataSource (Excel 드라이버) | Microsoft Docs"
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
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a4d5d0b2feb0a09aafeb441c6b33260e4f0738b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 하거나 다음 키워드에 동적으로 사용 하 여 데이터 원본을 삭제 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|DBQ|Microsoft Excel 드라이버의 Microsoft Excel 5.0 또는 이후 파일에 액세스할 때 통합 문서 파일의 이름입니다.<br /><br /> 동일한 옵션을 설정 하는이 **데이터베이스** 설정 대화 상자에서 합니다.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **디렉터리 선택** 또는 **통합 문서 선택** 설정 대화 상자에서 합니다.|  
|DESCRIPTION|데이터 원본의 데이터에 대 한 설명<br /><br /> 동일한 옵션을 설정 하는이 **설명** 설정 대화 상자에서 합니다.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버는 정수 ID입니다.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|파일 형식, 예를 들어 Excel 3.0, Excel 4.0, 5.0 Excel, Excel 7.0, Excel 97, Excel 2000 또는 Excel 2003입니다.|  
|FIRSTROWHASNAMES|범위의 첫 번째 행의 셀 또는 not (1) 테이블에 대 한 열 이름을 포함 하는지 여부를 나타냅니다 (0).|  
|MAXSCANROWS|기존 데이터에 따라 열의 데이터 형식을 설정할 때 검사할 행의 수입니다.<br /><br /> 검색할 행에 대 한 16 개가 하 1에서 숫자를 입력할 수 있습니다. 기본값은 8; 0으로 설정 하는 경우 모든 행이 검색 됩니다. (제한 벗어나는 숫자 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 하는이 **검색할 행** 설정 대화 상자에서 합니다.|  
|READONLY|파일을 만들기 위해 읽기 전용 이면 TRUE False 이면 읽기 전용 파일을 설정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **읽기 전용** 설정 대화 상자에서 합니다.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드 수를 지정 합니다. Microsoft Access 드라이버에 대 한이 값이 3, 기본적으로 사용 되지만 변경할 수 있습니다. DBASE, MicrosoftExceldriver이 값이 3, 이며 변경할 수 없습니다.<br /><br /> 동일한 옵션을 설정 하는이 **스레드** 설정 대화 상자에서 합니다.|
