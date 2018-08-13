---
title: 테이블 반환 매개 변수 (OLE DB) | Microsoft Docs
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
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5810dffa90bb93c7212e978449fc48ca842925c7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39545913"
---
# <a name="table-valued-parameters-ole-db"></a>테이블 반환 매개 변수(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  이 섹션에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 테이블 반환 매개 변수 지원에 대해 설명합니다. 추가 개요 정보를 참조 하세요 [테이블 반환 매개 변수 &#40;SQL Server Native Client&#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)합니다. 샘플을 보려면 [테이블 반환 매개 변수 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)합니다.  
  
## <a name="remarks"></a>Remarks  
 현재 매개 변수 집합(**ICommand::Execute**의 DBPARAMS 매개 변수)을 사용하여 다중 행 데이터를 프로시저에 대한 매개 변수로 서버에 보낼 수 있습니다. 매개 변수 집합을 사용할 경우 해당 집합의 모든 요소가 서버에 개별 RPC(원격 프로시저 호출) 요청으로 서버에 전송되어야 합니다. 테이블 반환 매개 변수는 유사한 기능을 제공하지만 서버와 더 밀접하게 통합됩니다. 따라서 RPC 요청 수가 감소하며 서버에서 집합 기반 작업을 사용할 수 있습니다.  
  
 테이블 반환 매개 변수가 지원 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자와 OLE DB **행 집합** 개체입니다. 모든 **행 집합** 소비자가 개체를 제공할 수 있습니다 (즉, 응용 프로그램 사용 하는 클라이언트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자) 매개 변수 테이블 반환 매개 변수에 대 한 자리 표시자로 합니다. 테이블 반환 매개 변수는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 매개 변수 유형과 마찬가지로 처리됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 생성, 검색, 지정, 바인딩 및 스키마 인터페이스를 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [테이블 반환 매개 변수 행 집합 만들기](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [테이블 반환 매개 변수 형식 검색](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [테이블 반환 매개 변수가 포함된 명령 실행](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [테이블 반환 매개 변수에 데이터 삽입](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수에 대해 변경된 스키마 행 집합](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원&#40;Methods&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [OLE DB 테이블 반환 매개 변수 형식 지원&#40;Properties&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [테이블 반환 매개 변수&#40;OLE DB&#41; 사용](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
