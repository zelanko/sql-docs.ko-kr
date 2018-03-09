---
title: "SQLTables (Access 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 895c4d86c11d88fcf544b9a3c7612e1a6cdf4764
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-access-driver"></a>SQLTables (Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버의 없기 때문에 NULL입니다. 와 *szTableOwner* NULL로 설정 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **SQLTables** 데이터베이스 파일의 경로 반환 합니다.|  
|*SzTableType*|Microsoft Access 드라이버를 사용 하는 경우 "시스템 테이블"는에 대 한 지원 *szTableType* 시스템 테이블에 대 한 "동의어"가 연결 된 테이블에 대 한 지원 및 "VIEW"가 행을 반환 하는 것에 대 한 지원 되는 쿼리 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLTables 함수](../../odbc/reference/syntax/sqltables-function.md)
