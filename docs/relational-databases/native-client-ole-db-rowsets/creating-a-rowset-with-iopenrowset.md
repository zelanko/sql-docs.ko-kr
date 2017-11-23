---
title: "IOpenRowset를 사용 하 여 행 집합 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c78658537d6af6bd08423aa2be3add03bdaba7b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-rowset-with-iopenrowset"></a>IOpenRowset을 사용하여 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 지원은 **iopenrowset:: Openrowset** 다음과 같은 제한 메서드:  
  
-   기본 테이블 또는 뷰의 지정 해야 합니다는 데이터베이스에서 ID (DBID) 구조체에서 *pTableID* 매개 변수를 가리킵니다.  
  
-   DBID *eKind* 멤버가 DBKIND_NAME을 나타내야 합니다.  
  
-   DBID *uName* 멤버는 유니코드 문자열과 기존의 기본 테이블 또는 뷰의 이름을 지정 해야 합니다.  
  
-   *pIndexID* 의 매개 변수 **OpenRowset** NULL 이어야 합니다.  
  
 결과 집합의 **iopenrowset:: Openrowset** 단일 행 집합을 포함 합니다. 단일 행 집합을 포함 하는 결과 집합에서 지원할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서입니다. 커서 지원을 통해 개발자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동시성 메커니즘을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
