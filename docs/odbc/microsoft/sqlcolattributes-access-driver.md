---
title: "SQLColAttributes (Access 드라이버) | Microsoft Docs"
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
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2531bbc58e55c3c58452701f1dd66ac6702a535
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|Attribute|설명|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|LONGVARBINARY 데이터 SQL_COLUMN_DISPLAY_SIZE 하지 2 시간 열의 최대 길이 열의 최대 길이입니다.|  
|SQL_OWNER_NAME|빈 문자열 ("") 소유자 이름입니다. 지원 되지 않으므로이 열에 반환 합니다.|  
|SQL_QUALIFIER_NAME|데이터베이스 파일의 경로를 반환 됩니다.|  
|SQL_COLUMN_SEARCHABLE|LONGVARCHAR 및 LONGVARBINARY 열 SQL_UNSEARCHABLE로 보고 됩니다.<br /><br /> 고정 길이 및 가변 길이 이진 및 문자 데이터 형식 LONGVARCHAR 및 LONGVARBINARY 없는 있지만 검색할 수 있는는.|  
  
> [!NOTE]  
>  위 그림은 하지 반환 하는 특성의 전체 목록은 **SQLColAttributes**합니다.

