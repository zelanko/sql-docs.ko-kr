---
title: "SQLConfigDataSource (텍스트 파일 드라이버) | Microsoft Docs"
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
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e781871cc8507d10617e1a147fa6d5a7c06ac756
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 하거나 다음 키워드에 동적으로 사용 하 여 데이터 원본을 삭제 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|CHARACTERSET|OEM 또는 ANSI 텍스트 드라이버입니다.|  
|COLNAMEHEADER|텍스트 드라이버에 대 한 데이터의 첫 번째 레코드를 열 이름 지정 여부를 나타냅니다. TRUE 또는 FALSE입니다.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.|  
|DESCRIPTION|데이터 원본의 데이터에 대 한 설명<br /><br /> 동일한 옵션을 설정 하는이 **설명** 설정 대화 상자에서 합니다.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버는 정수 ID입니다. 27 (텍스트)|  
|확장|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열합니다.<br /><br /> 동일한 옵션을 설정 하는이 **확장명 목록** 설정 대화 상자에서 합니다.|  
|FIL|텍스트 파일 형식|  
|파일 형식|텍스트 드라이버 (텍스트)에 대 한 파일 형식입니다.|  
|FORMAT|FIXEDLENGTH, TABDELIMITED, (쉼표), 여는 CSVDELIMITED 또는 (여는 괄호에 지정 된 특수 문자) DELIMITED() 텍스트 드라이버에 대 한 수 있습니다. 특수 문자 길이가 1 자 이며 문자 10 진수 또는 16 진수 형식 될 수 있습니다.|  
|MAXSCANROWS|기존 데이터에 따라 열의 데이터 형식을 설정할 때 검사할 행의 수입니다.<br /><br /> 텍스트 드라이버를 입력할 수 있는 숫자 1에서 32767 사이의; 검색할 행 수에 대 한 그러나 값은 기본적으로 항상 25입니다. (제한 벗어나는 숫자 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 하는이 **검색할 행** 설정 대화 상자에서 합니다.|  
|READONLY|파일을 만들기 위해 읽기 전용 이면 TRUE False 이면 읽기 전용 파일을 설정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **읽기 전용** 설정 대화 상자에서 합니다.|
