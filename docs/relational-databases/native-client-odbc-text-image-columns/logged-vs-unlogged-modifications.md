---
title: 기록되는 수정 및 수정 기록 되지 않는 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 91e832a0f2abdfea91a63f17414bf431e7275103
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128898"
---
# <a name="logged-vs-unlogged-modifications"></a>기록되는 수정 및 기록되지 않는 수정
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  응용 프로그램에서 요청 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 로그 아님 **텍스트**를 **ntext**, 및 **이미지** 수정 합니다. 하지만 이 옵션을 사용할 때는 주의해야 합니다. 경우에만 사용 해야 여기서 합니다 **텍스트**를 **ntext**, 또는 **이미지** 데이터가 중요 하지 않으며 데이터 소유자가 데이터를 복구 하는 기능 기꺼이 성능 향상  
  
 로깅을 **텍스트**, **ntext**, 및 **이미지** 호출 하 여 수정 제어 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 사용 하 여는  *특성* 매개 변수 SQL_SOPT_SS_ TEXTPTR_LOGGING로 설정 하 고 *ValuePtr* 변수와 SQL_TL_ON 또는 SQL_TL_OFF로 설정 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [text 및 image 열 관리](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
