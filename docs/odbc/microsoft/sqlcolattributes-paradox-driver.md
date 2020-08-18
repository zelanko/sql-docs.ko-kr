---
description: SQLColAttributes(Paradox 드라이버)
title: SQLColAttributes (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 016de4e65579b8218a73fb871071622adf0ce3de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412219"
---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|attribute|주석|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|가 중 데이터의 경우에는 열의 최대 길이가 열 시간 2의 최대 길이가 아니라 열의 최대 길이를 SQL_COLUMN_DISPLAY_SIZE 합니다.|  
|SQL_OWNER_NAME|소유자 이름이 지원 되지 않으므로이 열에 빈 문자열 ("")이 반환 됩니다.|  
|SQL_QUALIFIER_NAME|디렉터리에 대 한 경로가 반환 됩니다.|  
|SQL_COLUMN_SEARCHABLE|을 사용할 SQL_UNSEARCHABLE 수 없습니다.<br /><br /> 고정 길이 및 가변 길이 이진 및 문자 데이터 형식은 WVARBINARY 및 WVARCHAR가이 아닌 경우에도 검색할 수 있습니다.|  
  
> [!NOTE]  
>  위의는 **Sqlcolattributes**에서 반환 된 특성의 전체 목록이 아닙니다.
