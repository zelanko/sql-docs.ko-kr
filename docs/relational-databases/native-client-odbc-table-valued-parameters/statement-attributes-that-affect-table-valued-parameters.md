---
title: 테이블 반환 매개 변수에 영향을 주는 특성
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b4a6bfc8209946f6d550f243cc21a027c1f9fd6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760675"
---
# <a name="statement-attributes-that-affect-table-valued-parameters"></a>테이블 반환 매개 변수에 영향을 주는 문 특성
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  다음 표에서는 설명자 필드의 특성을 설명합니다.  
  
|특성 이름|형식|설명|  
|--------------------|----------|-----------------|  
|SQL_SOPT_SS_PARAM_FOCUS|SQLUINTEGER|SQL_SS_PARAM_FOCUS에 대 한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.|  
|SQL_SOPT_SS_NAME_SCOPE|SQLUINTEGER|SQL_SS_NAME_SCOPE에 대 한 자세한 내용은 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)를 참조 하세요.|  
||||

## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;테이블 반환 매개 변수](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
