---
title: SQL테이블(텍스트 파일 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299333"
---
# <a name="sqltables-text-file-driver"></a>SQLTables(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
|인수|주석|  
|--------------|--------------|  
|*szTable소유자*|*szTableOwner에* 대 한 유일한 유효한 인수는 NULL 드라이버 중 어느 것도 소유자 이름을 지원 하기 때문에 NULL입니다. *szTableOwner를* NULL로 설정하면 모든 테이블이 반환됩니다. null은 TABLE_OWNER 열에서 반환됩니다.|  
|*szTable한정자*|TABLE_QUALIFIER 열에서 **SQLTable** 디렉터리로 경로를 반환합니다.|  
|*스즈테이블 타입*|"TABLE"은 지원되는 유일한 테이블 유형입니다.<br /><br /> 텍스트 드라이버를 사용 하는 경우 **SQLTables에** 의해 반환 되는 파일 목록은 **ODBC 텍스트 설정** 대화 상자의 **확장 명세서** 상자의 파일 확장명에 의해 결정 됩니다.|
