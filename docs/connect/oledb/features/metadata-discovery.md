---
title: 메타 데이터 검색 | Microsoft Docs
description: SQL Server에 대 한 OLE DB 드라이버의 메타 데이터 검색
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9891e5708110be83a4ef33cb2a142accaf93ffe2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989065"
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항으로 인해 SQL Server용 OLE DB 드라이버 애플리케이션에서는 쿼리 실행 시 반환된 열 또는 매개 변수 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 일치하거나 호환되도록 지정할 수 있습니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 bcp 및 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 쿼리 출력 작업에서 메타데이터를 검색하지 않도록 지연된 읽기(지연된 메타데이터 검색)을 지정할 수 있습니다. 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 SQL Server용 OLE DB 드라이버를 사용하여 애플리케이션을 개발하지만 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이전 버전의 서버에 연결하는 경우 해당 서버 버전에 해당되는 메타데이터 검색 기능이 제공됩니다.  
  
## <a name="remarks"></a>Remarks   
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 OLE DB 멤버 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: GetParameterInfo (자세한 내용은 [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) 참조)  
  
 또한 IBCPSession::BCPSetBulkMode를 사용하여 메타데이터 형식을 지정하는 경우 향상된 성능을 경험할 수 있습니다.  
  
 에서 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]두 개의 저장 프로시저를 추가 하 여 SQL Server에 대 한 OLE DB 드라이버에서 향상 된 메타 데이터 검색을 수행할 수 있습니다.  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
