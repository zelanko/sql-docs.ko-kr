---
title: 책갈피 | Microsoft Docs
description: OLE DB Driver for SQL Server의 책갈피
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 26dfd57a44b11b3ca2dd748680c73f692308e05a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="bookmarks"></a>책갈피
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  소비자는 책갈피를 사용하여 신속하게 특정 행으로 돌아갈 수 있습니다. 즉, 소비자는 책갈피 값을 바탕으로 행에 임의로 액세스할 수 있습니다. 책갈피 열은 행 집합의 0번 열입니다. 소비자는 바인딩 구조의 dwFlag 필드 값을 DBCOLUMNSINFO_ISBOOKMARK로 설정하여 해당 열이 책갈피로 사용되는 행임을 지정합니다. 소비자는 또한 행 집합 속성 DBPROP_BOOKMARKS를 VARIANT_TRUE로 설정합니다. 이렇게 하면 행 집합에 0번 열을 지정할 수 있습니다. **irowsetlocate:: Getrowsat** 메서드는 다음 책갈피에서 오프셋으로 지정 된 행부터 행을 인출 하는 데 사용 됩니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
