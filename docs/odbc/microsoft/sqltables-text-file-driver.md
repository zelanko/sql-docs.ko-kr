---
title: SQLTables (텍스트 파일 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1299af287d9826893fc8c1f93007967509704d30
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811871"
---
# <a name="sqltables-text-file-driver"></a>SQLTables(텍스트 파일 드라이버)
> [!NOTE]  
>  이 항목에서는 텍스트 파일 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버 하나도 NULL입니다. 사용 하 여 *szTableOwner* NULL로 설정한 모든 테이블 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열의 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|"TABLE" 테이블 유형만 지원 됩니다.<br /><br /> 텍스트 드라이버를 사용 하는 경우, 반환한 파일의 목록을 **SQLTables** 의 파일 확장명에 따라 결정 됩니다 합니다 **확장 목록** 상자에 **ODBC 텍스트 설정** 대화 상자.|
