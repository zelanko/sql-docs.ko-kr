---
title: SQLTables (Paradox 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1108b06702a4753f0f99f6e67418fe8f54dc7de8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqltables-paradox-driver"></a>SQLTables (Paradox 드라이버)
> [!NOTE]  
>  이 항목에서는 Paradox 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|설명|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버의 없기 때문에 NULL입니다. 와 *szTableOwner* NULL로 설정 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|TABLE_QUALIFIER 열에서 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|Paradox 파일에 대 한 "TABLE"은 테이블 유형만 지원 합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [SQLTables 함수](../../odbc/reference/syntax/sqltables-function.md)
