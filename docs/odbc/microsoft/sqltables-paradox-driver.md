---
title: SQLTables (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c845bd2e5e3ec5e52cfd6d1c0891f8825af1e148
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735201"
---
# <a name="sqltables-paradox-driver"></a>SQLTables(Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버 하나도 NULL입니다. 사용 하 여 *szTableOwner* NULL로 설정한 모든 테이블 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열의 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|Paradox 파일에 대 한 "TABLE" 지원 되는 유일한 테이블 형식입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [SQLTables 함수](../../odbc/reference/syntax/sqltables-function.md)
