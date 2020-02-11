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
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054077"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 데이터 원본을 추가, 수정 또는 삭제 하는 데 사용 되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|CHARACTERSET|텍스트 드라이버의 경우 OEM 또는 ANSI입니다.|  
|COLNAMEHEADER|텍스트 드라이버의 경우 첫 번째 데이터 레코드에서 열 이름을 지정 하는지 여부를 나타냅니다. TRUE 또는 FALSE입니다.|  
|DEFAULTDIR|디렉터리에 대 한 경로 지정입니다.|  
|설명|데이터 원본의 데이터에 대 한 설명입니다.<br /><br /> 그러면 설정 대화 상자에서 **설명과** 동일한 옵션을 설정 합니다.|  
|DRIVER|드라이버 DLL에 대 한 경로 사양입니다.|  
|DRIVERID|드라이버의 정수 ID입니다. 27 (텍스트)|  
|확장할|데이터 원본에 있는 텍스트 파일의 파일 이름 확장명을 나열 합니다.<br /><br /> 그러면 설치 대화 상자에서 **확장명 목록과** 동일한 옵션을 설정 합니다.|  
|FIL|파일 형식 텍스트|  
|FILETYPE|텍스트 드라이버 (텍스트)의 파일 형식입니다.|  
|FORMAT|텍스트 드라이버의 경우는 FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (쉼표) 또는 구분 기호 () (괄호 안에 지정 된 특수 문자) 일 수 있습니다. 특수 문자는 한 문자 길이 이며 문자, 10 진수 또는 16 진수 형식일 수 있습니다.|  
|MAXSCANROWS|기존 데이터에 기반 하 여 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> 텍스트 드라이버의 경우 검색할 행 수에 대해 1에서 32767 사이의 숫자를 입력할 수 있습니다. 그러나이 값은 항상 기본값 25입니다. 제한 밖의 숫자는 오류를 반환 합니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **검색할 행** 과 동일한 옵션을 설정 합니다.|  
|READONLY|파일을 읽기 전용으로 설정 하려면 TRUE로 설정 합니다. FALSE 이면 파일을 읽기 전용으로 설정 합니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **읽기 전용** 과 동일한 옵션을 설정 합니다.|
