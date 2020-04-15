---
title: SQL절차 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ff76504c9a36657be60ba4855cf252474071d7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302374"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저는 값을 반환합니다. **SQL절차** 는 결과 집합 열 PROCEDURE_TYPE 대한 SQL_PT_FUNCTION 보고합니다.  
  
 **SQLProcedures는** *카탈로그 이름, 스키마 이름* 또는 *ProcName* 매개 변수에 대한 값이 있는지 여부를 SQL_SUCCESS 반환합니다. **SQLFetch는** 이러한 매개 변수에 잘못된 값이 사용되는 SQL_NO_DATA 반환합니다.  
  
 **SQL프로시저는** 정적 서버 커서에서 실행할 수 있습니다. 업데이터(동적 또는 키 집합) 커서에서 **SQLProcedures를** 실행하려는 시도는 커서 유형이 변경되었음을 나타내는 SQL_SUCCESS_WITH_INFO 반환합니다.  
  
 **SQLProcedures는** 이름이 *ProcName과* 일치하고 현재 사용자가 실행할 수 있거나 현재 사용자에게 VIEW 정의 권한이 부여된 프로시저에 대한 정보를 반환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL프로시저 기능](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 구현 정보](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
