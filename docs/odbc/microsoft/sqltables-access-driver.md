---
title: SQL테이블(액세스 드라이버) | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306094"
---
# <a name="sqltables-access-driver"></a>SQLTables(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
|인수|주석|  
|--------------|--------------|  
|*szTable소유자*|*szTableOwner에* 대 한 유일한 유효한 인수는 NULL 드라이버 중 어느 것도 소유자 이름을 지원 하기 때문에 NULL입니다. *szTableOwner를* NULL로 설정하면 모든 테이블이 반환됩니다. null은 TABLE_OWNER 열에서 반환됩니다.|  
|*szTable한정자*|TABLE_QUALIFIER 열에서 **SQLTable** 데이터베이스 파일에 대 한 경로를 반환 합니다.|  
|*스즈테이블 타입*|Microsoft Access 드라이버를 사용하는 경우 시스템 테이블의 *szTableType에* 대해 "SYSTEM TABLE"이 지원되고 연결된 테이블에 대해 "SYNONYM"이 지원되고 행 반환 쿼리에 대해 "VIEW"가 지원됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQLTables 함수](../../odbc/reference/syntax/sqltables-function.md)
