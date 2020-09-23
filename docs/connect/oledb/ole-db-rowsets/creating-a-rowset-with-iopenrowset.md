---
title: IOpenRowset을 사용하여 행 집합 만들기(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server가 행 집합 및 해당 사용에 대한 제한을 반환하도록 IOpenRowset::OpenRowset 메서드를 지원하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a39ff5a60f13a25c271be61d4db20a604364420
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862267"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>IOpenRowset을 사용하여 행 집합 만들기
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server는 다음과 같은 제한이 있는 **IOpenRowset::OpenRowset** 메서드를 지원합니다.  
  
-   데이터베이스 ID(DBID) 구조체에 *pTableID* 매개 변수가 가리키는 기본 테이블 또는 뷰를 지정해야 합니다.  
  
-   DBID *eKind* 멤버는 DBKIND_NAME을 나타내야 합니다.  
  
-   DBID *uName* 멤버는 기존의 기본 테이블 또는 뷰 이름을 유니코드 문자열로 지정해야 합니다.  
  
-   **OpenRowset**의 *pIndexID* 매개 변수는 NULL이어야 합니다.  
  
 **IOpenRowset::OpenRowset**의 결과 집합에는 단일 행 집합이 들어 있습니다. 단일 행 집합을 포함하는 결과 집합은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서에서 지원될 수 있습니다. 커서 지원을 통해 개발자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동시성 메커니즘을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
