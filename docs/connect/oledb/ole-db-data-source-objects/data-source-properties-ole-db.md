---
title: 데이터 원본 속성(OLE DB) | Microsoft Docs
description: 데이터 원본 속성(OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 13dd6afde96d42ac1fcc82b6fb24c721997b951d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "68015935"
---
# <a name="data-source-properties-ole-db"></a>데이터 원본 속성(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 다음과 같이 데이터 원본 속성을 구현합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/W: 읽기/쓰기 기본값: None<br /><br /> 설명: DBPROP_CURRENTCATALOG의 값은 OLE DB Driver for SQL Server 세션의 현재 데이터베이스를 보고합니다. 속성 값을 설정하면 [!INCLUDE[tsql](../../../includes/tsql-md.md)] USE *database* 문을 사용하여 현재 데이터베이스를 설정하는 것과 동일한 효과가 있습니다.<br /><br /> [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]부터는 [sp_defaultdb](../../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)를 호출하고 데이터베이스 이름을 소문자로 지정하면 데이터베이스가 원래 대/소문자가 섞인 이름으로 만들어진 경우에도 DBPROP_CURRENTCATALOG가 이름을 소문자로 반환합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 DBPROP_CURRENTCATALOG가 대/소문자가 섞인 이름을 반환했습니다.|  
|DBPROP_MULTIPLECONNECTIONS|R/W: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 연결이 행 집합을 생성하지 않거나 서버 커서가 아닌 행 집합을 생성하는 명령을 실행 중인 상태에서 사용자가 다른 명령을 실행하는 경우 DBPROP_MULTIPLECONNECTIONS가 VARIANT_TRUE이면 새 명령을 실행하기 위해 새 연결이 생성됩니다.<br /><br /> DBPROP_MULTIPLECONNECTION이 VARIANT_FALSE이거나 연결에 트랜잭션이 활성화된 경우 SQL Server용 OLE DB 드라이버는 다른 연결을 만들지 않습니다. SQL Server용 OLE DB 드라이버는 DBPROP_MULTIPLECONNECTIONS가 VARIANT_FALSE이면 DB_E_OBJECTOPEN을 반환하고, 활성 트랜잭션이 있으면 E_FAIL을 반환합니다. 트랜잭션 및 잠금은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]가 연결별로 관리합니다. 두 번째 연결이 생성되면 분리된 연결에 대한 명령은 잠금을 공유하지 않습니다. 한 명령이 다른 명령을 차단하지 않도록 다른 명령이 요청한 행의 잠금은 유지됩니다. 여러 세션을 만들 때도 마찬가지입니다.<br /><br /> 각 세션이 별도의 연결을 가집니다.|  
  
 SQL Server용 OLE DB 드라이버는 공급자별 속성 집합 DBPROPSET_SQLSERVERDATASOURCE에 다음과 같은 추가 데이터 원본 속성을 정의합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/W: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 메모리에서 대량 복사를 사용하려면 SSPROP_ENABLEFASTLOAD 속성을 VARIANT_TRUE로 설정해야 합니다. 데이터 원본에서 이 속성을 설정하면 새로 생성되는 세션에서 소비자의 [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스 액세스를 허용합니다.<br /><br /> 속성을 VARIANT_TRUE로 설정하면 **IID_IRowsetFastLoad** 인터페이스를 요청하거나 **SSPROP_IRowsetFastLoad**를 VARIANT_TRUE로 설정하여 **IOpenRowset::OpenRowset**을 통해 **IRowsetFastLoad** 인터페이스를 사용할 수 있습니다.|  
|SSPROP_ENABLEBULKCOPY|R/W: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 파일에서 대량 복사를 사용하려면 SSPROP_ENABLEBULKCOPY 속성을 VARIANT_TRUE로 설정해야 합니다. 데이터 원본에서 이 속성을 설정하면 소비자가 세션과 동일한 수준에서 IBCPSession 인터페이스에 액세스할 수 있습니다.<br /><br /> SSPROP_IRowsetFastLoad도 VARIANT_TRUE로 설정해야 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
