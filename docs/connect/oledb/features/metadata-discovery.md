---
title: 메타데이터 검색 | Microsoft Docs
description: OLE DB Driver for SQL Server 애플리케이션에서 메타데이터 호환성을 보장할 수 있는 메타데이터 검색 기능 향상에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: adccad510a1126173e44015e6ecd60a90a32550b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861474"
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항으로 인해 SQL Server용 OLE DB 드라이버 애플리케이션에서는 쿼리 실행 시 반환된 열 또는 매개 변수 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 일치하거나 호환되도록 지정할 수 있습니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 bcp 및 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 쿼리 출력 작업에서 메타데이터를 검색하지 않도록 지연된 읽기(지연된 메타데이터 검색)을 지정할 수 있습니다. 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 SQL Server용 OLE DB 드라이버를 사용하여 애플리케이션을 개발하지만 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이전 버전의 서버에 연결하는 경우 해당 서버 버전에 해당되는 메타데이터 검색 기능이 제공됩니다.  
  
## <a name="remarks"></a>설명   
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 OLE DB 멤버 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters::GetParameterInfo(자세한 내용은 [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) 참조)  
  
 또한 IBCPSession::BCPSetBulkMode를 사용하여 메타데이터 형식을 지정하는 경우 향상된 성능을 경험할 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 다음과 같은 두 개의 저장 프로시저가 추가되어 OLE DB Driver for SQL Server에서 메타데이터 검색 기능이 향상되었습니다.  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
