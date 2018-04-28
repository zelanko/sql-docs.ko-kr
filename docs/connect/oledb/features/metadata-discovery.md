---
title: 메타 데이터 검색 | Microsoft Docs
description: OLE DB 드라이버에서 SQL Server에 대 한 메타 데이터 검색
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d51740f1ca6780f0f3c13d48ec4dd2d0c3f7ff21
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="metadata-discovery"></a>메타데이터 검색
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  메타 데이터 검색 개선 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] OLE DB Driver for SQL Server 응용 프로그램을 해당 열을 허용 또는 쿼리 실행에서 반환 된 매개 변수 메타 데이터는 동일 하거나 하기 전에 지정한 메타 데이터 형식과 호환 쿼리를 실행 합니다. 쿼리 실행 후 반환된 메타데이터가 쿼리를 실행하기 전에 지정한 메타데이터 형식과 호환되지 않는 경우 오류가 발생합니다.  
  
 Bcp 및 IBCPSession 및 IBCPSession2 인터페이스에서는 이제 지정할 수 있습니다는 지연 된 쿼리 출력 작업에 대 한 메타 데이터 검색을 방지 하기 위해 읽기 (지연 된 메타 데이터 검색). 이로 인해 성능이 향상되고 메타데이터 검색 오류가 발생하지 않습니다.  
  
 SQL Server 용 OLE DB 드라이버를 사용 하 여 응용 프로그램을 개발 하지만 서버 버전에 연결 하는 경우 보다 이전 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], 메타 데이터 검색 기능이 서버 버전에 해당 됩니다.  
  
## <a name="remarks"></a>주의   
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에서 다음 OLE DB 멤버 함수의 기능이 개선되어 메타데이터 검색 기능이 향상되었습니다.  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   Icommandwithparameters:: Getparameterinfo (참조 [ICommandWithParameters](../../oledb/ole-db-interfaces/icommandwithparameters.md) 자세한 내용은)  
  
 IBCPSession::BCPSetBulkMode를 사용 하 여 메타 데이터 형식 지정 하는 경우에 성능이 향상 될 됩니다.  
  
 OLE DB 드라이버에서 SQL Server에 대 한 향상 된 메타 데이터 검색은 두 개의 저장된 프로시저에 추가 되어 가능한 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
