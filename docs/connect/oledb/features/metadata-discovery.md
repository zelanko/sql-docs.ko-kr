---
title: 메타 데이터 검색 | Microsoft Docs
description: OLE DB 드라이버에서 SQL Server에 대 한 메타 데이터 검색
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: c32d932f65f0e4c34eb3ac58d3124d7e5afcc738
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033446"
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서의 메타데이터 검색 개선 사항으로 인해 SQL Server용 OLE DB 드라이버 응용 프로그램에서는 쿼리 실행 시 반환된 열 또는 매개 변수 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 일치하거나 호환되도록 지정할 수 있습니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 bcp 및 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 쿼리 출력 작업에서 메타데이터를 검색하지 않도록 지연된 읽기(지연된 메타데이터 검색)을 지정할 수 있습니다. 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 SQL Server용 OLE DB 드라이버를 사용하여 응용 프로그램을 개발하지만 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 이전 버전의 서버에 연결하는 경우 해당 서버 버전에 해당되는 메타데이터 검색 기능이 제공됩니다.  
  
## <a name="remarks"></a>Remarks   
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 OLE DB 멤버 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   Icommandwithparameters:: Getparameterinfo (참조 [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) 자세한)  
  
 또한 IBCPSession::BCPSetBulkMode를 사용하여 메타데이터 형식을 지정하는 경우 향상된 성능을 경험할 수 있습니다.  
  
 OLE DB 드라이버에서 SQL Server에 대 한 향상 된 메타 데이터 검색 되어 있는 두 개의 저장된 프로시저의 추가 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
