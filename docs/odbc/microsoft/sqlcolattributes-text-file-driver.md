---
title: SQLColAttributes (텍스트 파일 드라이버) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColAttributes
- SQLColAttribute function [ODBC], Text File Driver
ms.assetid: 132fd1c0-1921-4a7d-910e-aedf1bff5453
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eafe02ba76dcaa6078abee862d743deb4765bdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307924"
---
# <a name="sqlcolattributes-text-file-driver"></a>SQLColAttributes(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
|특성|주석|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|LONGVARBINARY 데이터의 경우 SQL_COLUMN_DISPLAY_SIZE 열의 최대 길이가 아니라 열 시간 2의 최대 길이입니다.|  
|SQL_OWNER_NAME|소유자 이름이 지원되지 않으므로 빈 문자열("")이 이 열에서 반환됩니다.|  
|SQL_QUALIFIER_NAME|디렉터리로 가는 경로가 반환됩니다.|  
|SQL_COLUMN_SEARCHABLE|롱바르바이너리 및 롱바르차르 열은 SQL_UNSEARCHABLE 것으로 보고됩니다.<br /><br /> LONGVARBINARY 및 LONGVARCHAR는 아니지만 고정 길이 및 가변 길이 바이너리 및 문자 데이터 형식은 검색 할 수 있습니다.|
