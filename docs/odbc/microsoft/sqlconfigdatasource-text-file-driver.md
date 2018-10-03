---
title: SQLConfigDataSource (텍스트 파일 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1635538f69b313a73a24ab1531f8793c7d98741e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612661"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 합니다 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 또는 데이터 원본 삭제 동적으로 다음과 같은 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|CHARACTERSET|OEM 또는 ANSI 텍스트 드라이버입니다.|  
|COLNAMEHEADER|텍스트 드라이버에 대 한 데이터의 첫 번째 레코드 열 이름을 지정 하는지 여부를 나타냅니다. TRUE 또는 FALSE입니다.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.|  
|DESCRIPTION|데이터 원본에 있는 데이터의 설명입니다.<br /><br /> 동일한 옵션을 설정 **설명을** 설정 대화 상자에서.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버에 대 한 정수 ID입니다. 27 (텍스트)|  
|확장|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열합니다.<br /><br /> 동일한 옵션을 설정 **확장 목록** 설정 대화 상자에서.|  
|FIL|텍스트 파일 형식|  
|파일 형식|(텍스트) 텍스트 드라이버에 대 한 파일 형식입니다.|  
|FORMAT|FIXEDLENGTH, TABDELIMITED, (쉼표), 여 CSVDELIMITED 또는 (여는 괄호 안에 지정 된 특수 문자) DELIMITED() 텍스트 드라이버의 경우 수 있습니다. 특수 문자 1 자 길이 이며 문자가 10 진수 또는 16 진수 형식에 있을 수 있습니다.|  
|MAXSCANROWS|기존 데이터를 기반으로 하는 열의 데이터 형식을 설정 하는 경우 검색할 행의 수입니다.<br /><br /> 텍스트 드라이버를 입력할 수 있습니다 숫자 1에서 32767 사이의; 검색할 행의 수에 대 한 그러나 값은 기본적으로 항상 25입니다. (제한 벗어나는 숫자로 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 **검색할 행** 설정 대화 상자에서.|  
|READONLY|읽기 전용 파일을 확인. 읽기 전용 파일을 만들기 위해 FALSE입니다.<br /><br /> 동일한 옵션을 설정 **읽기 전용** 설정 대화 상자에서.|
