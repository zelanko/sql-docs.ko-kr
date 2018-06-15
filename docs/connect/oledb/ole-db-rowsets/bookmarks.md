---
title: 책갈피 | Microsoft Docs
description: OLE DB Driver for SQL Server의 책갈피
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 3e7c40b7d81be7c94c6e99c777006bfda7355f25
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305632"
---
# <a name="bookmarks"></a>책갈피
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  소비자는 책갈피를 사용하여 신속하게 특정 행으로 돌아갈 수 있습니다. 즉, 소비자는 책갈피 값을 바탕으로 행에 임의로 액세스할 수 있습니다. 책갈피 열은 행 집합의 0번 열입니다. 소비자는 바인딩 구조의 dwFlag 필드 값을 DBCOLUMNSINFO_ISBOOKMARK로 설정하여 해당 열이 책갈피로 사용되는 행임을 지정합니다. 소비자는 또한 행 집합 속성 DBPROP_BOOKMARKS를 VARIANT_TRUE로 설정합니다. 이렇게 하면 행 집합에 0번 열을 지정할 수 있습니다. **irowsetlocate:: Getrowsat** 메서드는 다음 책갈피에서 오프셋으로 지정 된 행부터 행을 인출 하는 데 사용 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
