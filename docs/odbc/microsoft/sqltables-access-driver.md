---
title: SQLTables (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306094"
---
# <a name="sqltables-access-driver"></a>SQLTables(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
|인수|주석|  
|--------------|--------------|  
|*szTableOwner*|모든 드라이버가 소유자 이름을 지원 하지 않으므로 *Sztableowner* 에 대해 올바른 인수는 NULL입니다. *Sztableowner* 를 NULL로 설정 하면 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **Sqltables** 는 데이터베이스 파일에 대 한 경로를 반환 합니다.|  
|*SzTableType*|Microsoft Access 드라이버를 사용 하는 경우 "시스템 테이블"이 시스템 테이블에 대해 *szTableType* 지원 되 고, "동의어"가 연결 된 테이블에 대해 지원 되며, 행 반환 쿼리에 대해 "VIEW"가 지원 됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQLTables 함수](../../odbc/reference/syntax/sqltables-function.md)
