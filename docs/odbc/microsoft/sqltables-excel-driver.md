---
title: SQLTables (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89157178aa9c134bdb1b9518343007adb1e1e05f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132419"
---
# <a name="sqltables-excel-driver"></a>SQLTables(Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버 하나도 NULL입니다. 사용 하 여 *szTableOwner* NULL로 설정한 모든 테이블 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|경우는 Microsoft Excel 3.0 또는 4.0 드라이버는를 호출 하는 경우 **SQLTables** 에 대 한 값을 사용 하 여 *szTableQualifier* 기존 테이블의 이름 없는, 드라이버는 해당 이름의 테이블이 만들어집니다.<br /><br /> TABLE_QUALIFIER 열의 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|Microsoft Excel 3.0 또는 4.0에 대 한 "TABLE" 테이블 유형만 지원 됩니다.<br /><br /> Microsoft Excel 파일의 이후 버전에 "시스템 테이블" 시트 이름 (테이블 끝에 "$"로)에 대 한 돌아가고 "TABLE" 워크시트 내의 테이블에 대해 반환 됩니다.|
