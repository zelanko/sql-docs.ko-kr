---
title: SQLConfigData원본 (텍스트 파일 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283923"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 데이터 원본을 동적으로 추가, 수정 또는 삭제하는 데 사용되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|문자 집합|텍스트 드라이버, OEM 또는 ANSI의 경우.|  
|콜네임헤더|Text 드라이버의 경우 데이터의 첫 번째 레코드가 열 이름을 지정할지 여부를 나타냅니다. TRUE 또는 FALSE.|  
|기본디더|디렉터리로의 경로 사양입니다.|  
|설명|데이터 원본의 데이터에 대한 설명입니다.<br /><br /> 이렇게 하면 설정 대화 상자의 **설명과** 동일한 옵션이 설정됩니다.|  
|DRIVER|드라이버 DLL에 대한 경로 사양입니다.|  
|드라이버 ID|드라이버에 대한 정수 ID입니다. 27 (텍스트)|  
|확장|데이터 원본에 텍스트 파일의 파일 이름 확장명을 나열합니다.<br /><br /> 이렇게 하면 설치 대화 상자의 **확장 목록과** 동일한 옵션이 설정됩니다.|  
|Fil|파일 형식 텍스트|  
|Filetype|텍스트 드라이버(텍스트)에 대한 파일 형식입니다.|  
|FORMAT|텍스트 드라이버의 경우 고정 길이, TABDELIMITED, CSVDELIMITED (쉼표로) 또는 DELIMITED () (괄호에 지정된 특수 문자에 의해)할 수 있습니다. 특수 문자는 길이가 하나의 문자이며 문자, 소수점 또는 육각형 형식일 수 있습니다.|  
|맥스칸로우스|기존 데이터를 기반으로 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> Text 드라이버의 경우 검색할 행 수에 대해 1에서 32767까지 숫자를 입력할 수 있습니다. 그러나 값은 항상 25로 기본값입니다. (한계를 벗어난 숫자는 오류를 반환합니다.)<br /><br /> 이렇게 하면 설정 대화 상자에서 **검색할 행과** 동일한 옵션이 설정됩니다.|  
|READONLY|TRUE는 파일을 읽기 전용으로 만듭니다. FALSE파일을 읽기 전용으로 만들지 않도록 합니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **만 읽기와** 동일한 옵션이 설정됩니다.|
