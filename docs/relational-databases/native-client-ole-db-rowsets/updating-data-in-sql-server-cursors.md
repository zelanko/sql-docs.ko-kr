---
title: SQL Server 커서의 데이터를 업데이트 | Microsoft 문서
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
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d68010d755051276bdce49e9ff623a70124aee30
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39541083"
---
# <a name="updating-data-in-sql-server-cursors"></a>SQL Server 커서의 데이터 업데이트
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  통해 데이터 페치 및 업데이트 하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 같은 고려 사항 및 클라이언트 응용 프로그램에 적용 되는 제약 조건에 의해 네이티브 클라이언트 OLE DB 공급자 소비자 응용 프로그램이 바인딩되어 있습니다.  
  
 동시 데이터 액세스 제어에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서의 행만 참여합니다. 소비자가 수정이 가능한 행 집합을 요청하면 DBPROP_LOCKMODE에서 동시성 제어를 관리합니다. 소비자는 행 집합을 열기 전에 DBPROP_LOCKMODE 속성을 설정하여 동시 액세스 제어의 수준을 변경합니다.  
  
 트랜잭션이 오랫동안 열려 있을 수 있도록 설계된 클라이언트 응용 프로그램의 경우 트랜잭션 격리 수준 때문에 행 위치 지정에 상당한 시간 지연이 발생할 수 있습니다. 기본적으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자를 사용 하 여 DBPROPVAL_TI_READCOMMITTED에서 지정 하는 커밋된 읽기 격리 수준입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 행 집합 동시성 읽기 전용일 때 커밋되지 않은 읽기 격리를 지원 합니다. 따라서 소비자는 수정이 가능한 행 집합에 더 높은 수준의 격리를 요청할 수 있지만 더 낮은 수준은 요청할 수 없습니다.  
  
## <a name="immediate-and-delayed-update-modes"></a>즉시 및 지연 업데이트 모드  
 즉시 업데이트 모드에서는 **IRowsetChange::SetData**를 호출할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 왕복이 발생합니다. 소비자가 단일 행을 여러 번 변경한 경우 **SetData**를 한 번 호출하여 모든 변경 내용을 전송하는 것이 효율적입니다.  
  
 지연 업데이트 모드에서는 **IRowsetUpdate::Update**의 *cRows* 및 *rghRows* 매개 변수에 지정된 각 행에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로의 왕복이 수행됩니다.  
  
 두 모드 모두 왕복은 행 집합에 대해 열려 있는 트랜잭션 개체가 없는 경우 고유한 트랜잭션을 나타냅니다.  
  
 사용 하는 **IRowsetUpdate::Update**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자가 지정 된 각 행을 처리 합니다. 머무르지 행에 대 한 데이터, 길이, 또는 상태에 대 한 잘못 된 값으로 인해 발생 하는 동안 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 처리 하는 네이티브 클라이언트 OLE DB 공급자입니다. 업데이트에 참여하는 행은 모두 수정되거나 전혀 수정되지 않습니다. 소비자 검사 해야 하는 반환 된 *prgRowStatus* 배열의 특정에 대 한 오류 확인을 경우 행은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 네이티브 클라이언트 OLE DB 공급자는 DB_S_ERRORSOCCURRED를 반환 합니다.  
  
 소비자는 행이 특정한 순서로 처리된다고 가정해서는 안 됩니다. 소비자가 두 개 이상의 행에서 수정된 데이터를 순서대로 처리해야 하는 경우에는 응용 프로그램 논리에서 이러한 순서를 설정하고 트랜잭션을 열어 여기에 프로세스를 넣어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 집합의 데이터 업데이트](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
