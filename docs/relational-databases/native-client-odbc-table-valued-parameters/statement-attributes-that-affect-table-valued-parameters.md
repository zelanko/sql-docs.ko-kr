---
title: 테이블 반환 매개 변수에 영향을 주는 문 특성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor header field
- table-valued parameters (ODBC), statement attribute
ms.assetid: 089213b0-d368-4332-b2e5-b2bd8770c64f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e79459d0931866840efe19d87d6d264ce6f46b5d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73775681"
---
# <a name="statement-attributes-that-affect-table-valued-parameters"></a>테이블 반환 매개 변수에 영향을 주는 문 특성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  다음 표에서는 설명자 필드의 특성을 설명합니다.  
  
|특성 이름|형식|설명|  
|--------------------|----------|-----------------|  
|SQL_SOPT_SS_PARAM_FOCUS|SQLUINTEGER|SQL_SS_PARAM_FOCUS에 대 한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.|  
|SQL_SOPT_SS_NAME_SCOPE|SQLUINTEGER|SQL_SS_NAME_SCOPE에 대 한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC 테이블 반환 매개 &#40;변수&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
