---
title: IDBProperties (OLE DB) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 298edcb5a9ea05ad4a76ddd27461771e6098ca5f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39547853"
---
# <a name="idbproperties-ole-db"></a>IDBProperties(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  OLE DB 표준 사양을 통해 공급자가 **DBPROPINFO::vValues**에 대해 VT_EMPTY를 지정할 수 있습니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB는 항상 VT_EMPTY를 반환를 호출할 때 **idbproperties:: Getpropertyinfo** 사용 하 여 **DBPROPSET_ROWSETALL** 행 집합 속성을 검색 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [인터페이스 &#40;OLE DB&#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
