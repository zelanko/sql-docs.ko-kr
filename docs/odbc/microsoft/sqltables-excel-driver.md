---
title: "SQLTables (Excel 드라이버) | Microsoft Docs"
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
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9aad9b74b9813c0526df87437999b66f27e95414
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-excel-driver"></a>SQLTables (Excel 드라이버)
> [!NOTE]  
>  이 항목에서는 Excel 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
|인수|설명|  
|--------------|--------------|  
|*szTableOwner*|에 대 한 유효한 인수 *szTableOwner* 소유자 이름을 지 원하는 드라이버의 없기 때문에 NULL입니다. 와 *szTableOwner* NULL로 설정 모든 테이블이 반환 됩니다. TABLE_OWNER 열에 NULL이 반환 됩니다.|  
|*szTableQualifier*|Microsoft Excel 3.0 또는 4.0 드라이버 사용 되는 경우를 호출 하는 경우 **SQLTables** 에 값이 있는 *szTableQualifier* 기존 테이블의 이름을 즉, 드라이버는 해당 이름의 테이블이 만들어집니다.<br /><br /> TABLE_QUALIFIER 열에서 **SQLTables** 디렉터리 경로 반환 합니다.|  
|*SzTableType*|Microsoft Excel 3.0 또는 4.0에 대 한 "TABLE" 지원만 테이블 유형입니다.<br /><br /> Microsoft Excel 파일의 이후 버전에서는 시트 이름 (테이블 끝에 "$"로)에 대해 "시스템 테이블"이 반환 하 고 "TABLE" 워크시트 내의 테이블에 대 한 반환 됩니다.|

