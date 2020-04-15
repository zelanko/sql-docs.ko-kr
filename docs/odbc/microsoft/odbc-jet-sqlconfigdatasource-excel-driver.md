---
title: ODBC 제트 SQLConfigDataSource (엑셀 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293013"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 데이터 원본을 동적으로 추가, 수정 또는 삭제하는 데 사용되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|DBQ|마이크로 소프트 엑셀 드라이버의 경우 마이크로 소프트 엑셀 5.0 이상 파일, 통합 문서 파일의 이름.<br /><br /> 이렇게 하면 설정 대화 상자의 **데이터베이스와** 동일한 옵션이 설정됩니다.|  
|기본디더|디렉터리로의 경로 사양입니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **디렉터리 선택** 또는 **통합 문서 선택과** 동일한 옵션이 설정됩니다.|  
|설명|데이터 원본의 데이터에 대한 설명입니다.<br /><br /> 이렇게 하면 설정 대화 상자의 **설명과** 동일한 옵션이 설정됩니다.|  
|DRIVER|드라이버 DLL에 대한 경로 사양입니다.|  
|드라이버 ID|드라이버에 대한 정수 ID입니다.<br /><br /> 534 (마이크로 소프트 엑셀 3.0)<br /><br /> 278 (마이크로 소프트 엑셀 4.0)<br /><br /> 22 (마이크로 소프트 엑셀 5.0 / 7.0)<br /><br /> 790 (마이크로 소프트 엑셀 97-2003)|  
|Fil|파일 형식, 예를 들어, 엑셀 3.0, 엑셀 4.0, 엑셀 5.0, 엑셀 7.0, 엑셀 97, 엑셀 2000, 또는 엑셀 2003.|  
|퍼스트로하스네임|범위의 첫 번째 행의 셀에 테이블(1)에 대한 열 이름이 포함되어 있는지 여부(0)를 나타냅니다.|  
|맥스칸로우스|기존 데이터를 기반으로 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> 행을 스캔하려면 1에서 16까지의 숫자를 입력할 수 있습니다. 값은 기본값은 8입니다. 0으로 설정하면 모든 행이 검색됩니다. (한계를 벗어난 숫자는 오류를 반환합니다.)<br /><br /> 이렇게 하면 설정 대화 상자에서 **검색할 행과** 동일한 옵션이 설정됩니다.|  
|READONLY|TRUE는 파일을 읽기 전용으로 만듭니다. FALSE파일을 읽기 전용으로 만들지 않도록 합니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **만 읽기와** 동일한 옵션이 설정됩니다.|  
|스레드|사용할 엔진의 배경 스레드 수입니다. Microsoft Access 드라이버의 경우 이 값은 기본값3이지만 변경할 수 있습니다. dBASE의 경우 MicrosoftExceldriver는 이 값이 3이며 변경할 수 없습니다.<br /><br /> 이렇게 하면 설정 대화 상자의 스레드와 동일한 옵션이 **설정됩니다.**|
