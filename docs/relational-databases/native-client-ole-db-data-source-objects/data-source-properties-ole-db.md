---
title: 데이터 원본 속성 (OLE DB) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 6e14fefc-4e0b-4847-a833-4cf0abe65d50
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9932fbcdcfc1a45432130d7111a5583fa5e5288b
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102448"
---
# <a name="data-source-properties-ole-db"></a>데이터 원본 속성(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 데이터 원본 속성을 다음과 같이 구현 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|DBPROP_CURRENTCATALOG|R/w: 읽기/쓰기 기본값: 없음<br /><br /> 설명: DBPROP_CURRENTCATALOG 값에 대 한 현재 데이터베이스를 보고 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션입니다. 속성 값을 설정하면 [!INCLUDE[tsql](../../includes/tsql-md.md)] USE *database* 문을 사용하여 현재 데이터베이스를 설정하는 것과 동일한 효과가 있습니다.<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)를 호출하고 데이터베이스 이름을 소문자로 지정하면 데이터베이스가 원래 대/소문자가 섞인 이름으로 만들어진 경우에도 DBPROP_CURRENTCATALOG가 이름을 소문자로 반환합니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 DBPROP_CURRENTCATALOG가 대/소문자가 섞인 이름을 반환했습니다.|  
|DBPROP_MULTIPLECONNECTIONS|R/w: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 연결이 행 집합을 생성하지 않거나 서버 커서가 아닌 행 집합을 생성하는 명령을 실행 중인 상태에서 사용자가 다른 명령을 실행하는 경우 DBPROP_MULTIPLECONNECTIONS가 VARIANT_TRUE이면 새 명령을 실행하기 위해 새 연결이 생성됩니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_MULTIPLECONNECTION이 VARIANT_FALSE 또는 연결에는 트랜잭션이 활성화 된 경우 Native Client OLE DB 공급자는 다른 연결을 만들지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 DBPROP_MULTIPLECONNECTIONS가 VARIANT_FALSE 및 활성 트랜잭션이 있으면 E_FAIL을 반환 하는 경우 DB_E_OBJECTOPEN을 반환 합니다. 트랜잭션 및 잠금은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 연결별로 관리합니다. 두 번째 연결이 생성되면 분리된 연결에 대한 명령은 잠금을 공유하지 않습니다. 한 명령이 다른 명령을 차단하지 않도록 다른 명령이 요청한 행의 잠금은 유지됩니다. 여러 세션을 만들 때도 마찬가지입니다.<br /><br /> 각 세션이 별도의 연결을 가집니다.|  
  
 공급자별 속성 집합 dbpropset_sqlserverdatasource에 다음과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음 추가 데이터 원본 속성을 정의 합니다.  
  
|속성 ID|Description|  
|-----------------|-----------------|  
|SSPROP_ENABLEFASTLOAD|R/w: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 메모리에서 대량 복사를 사용하려면 SSPROP_ENABLEFASTLOAD 속성을 VARIANT_TRUE로 설정해야 합니다. 데이터 원본에서 이 속성을 설정하면 새로 생성되는 세션에서 소비자의 [IRowsetFastLoad](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) 인터페이스 액세스를 허용합니다.<br /><br /> 속성을 VARIANT_TRUE로 설정하면 **IID_IRowsetFastLoad** 인터페이스를 요청하거나 **SSPROP_IRowsetFastLoad**를 VARIANT_TRUE로 설정하여 **IOpenRowset::OpenRowset**을 통해 **IRowsetFastLoad** 인터페이스를 사용할 수 있습니다.|  
|SSPROP_ENABLEBULKCOPY|R/w: 읽기/쓰기 기본값: VARIANT_FALSE<br /><br /> 설명: 파일에서 대량 복사를 사용하려면 SSPROP_ENABLEBULKCOPY 속성을 VARIANT_TRUE로 설정해야 합니다. 데이터 원본에서 이 속성을 설정하면 소비자가 세션과 동일한 수준에서 IBCPSession 인터페이스에 액세스할 수 있습니다.<br /><br /> SSPROP_IRowsetFastLoad도 VARIANT_TRUE로 설정해야 합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 원본 개체 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
