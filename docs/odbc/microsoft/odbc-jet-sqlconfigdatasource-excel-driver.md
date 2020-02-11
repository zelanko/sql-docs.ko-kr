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
ms.openlocfilehash: ab33bfdef2b633cd5a7a3e215a3f6522d8d664ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915707"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 데이터 원본을 추가, 수정 또는 삭제 하는 데 사용 되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|DBQ|Microsoft excel driver For Microsoft Excel 5.0 이상 파일에 액세스할 때 통합 문서 파일의 이름입니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **데이터베이스** 와 동일한 옵션을 설정 합니다.|  
|DEFAULTDIR|디렉터리에 대 한 경로 지정입니다.<br /><br /> 그러면 설정 대화 상자에서 **디렉터리 선택** 또는 **통합 문서 선택** 과 동일한 옵션이 설정 됩니다.|  
|설명|데이터 원본의 데이터에 대 한 설명입니다.<br /><br /> 그러면 설정 대화 상자에서 **설명과** 동일한 옵션을 설정 합니다.|  
|DRIVER|드라이버 DLL에 대 한 경로 사양입니다.|  
|DRIVERID|드라이버의 정수 ID입니다.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|파일 형식 (예: Excel 3.0, Excel 4.0, Excel 5.0, Excel 7.0, Excel 97, Excel 2000 또는 Excel 2003).|  
|FIRSTROWHASNAMES|범위에 있는 첫 번째 행의 셀에 테이블의 열 이름 (1)이 포함 되어 있는지 (0) 여부를 나타냅니다.|  
|MAXSCANROWS|기존 데이터에 기반 하 여 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> 검색할 행에 대해 1에서 16 사이의 숫자를 입력할 수 있습니다. 값의 기본값은 8입니다. 0으로 설정 하면 모든 행이 검색 됩니다. 제한 밖의 숫자는 오류를 반환 합니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **검색할 행** 과 동일한 옵션을 설정 합니다.|  
|READONLY|파일을 읽기 전용으로 설정 하려면 TRUE로 설정 합니다. FALSE 이면 파일을 읽기 전용으로 설정 합니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **읽기 전용** 과 동일한 옵션을 설정 합니다.|  
|임계값|엔진에서 사용할 백그라운드 스레드 수입니다. Microsoft Access driver의 경우이 값의 기본값은 3 이지만 변경할 수 있습니다. DBASE의 경우이 값은 3 MicrosoftExceldriver 변경할 수 없습니다.<br /><br /> 설정 대화 상자에서 **스레드와** 동일한 옵션을 설정 합니다.|
