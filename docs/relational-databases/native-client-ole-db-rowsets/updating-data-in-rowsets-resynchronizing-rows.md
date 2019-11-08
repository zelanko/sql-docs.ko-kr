---
title: 행 다시 동기화 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd994f7ec89f154f106df25190819b227495f290
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788729"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>행 집합의 데이터 업데이트 - 행 다시 동기화
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서 지원 행 집합에 대해서만 **IRowsetResynch** 을 지원 합니다. **IRowsetResynch**는 요청 시 사용할 수 없으며 소비자가 행 집합을 열기 전에 이 인터페이스를 요청해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합의 데이터 업데이트](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
