---
title: IOpenRowset을 사용 하 여 행 집합 만들기 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버의 IOpenRowset 인터페이스를 사용 하 여 행 집합 만들기
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 78b08a3da3da89e0db0d801945416dcdb1ff9c03
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799213"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>IOpenRowset을 사용하여 행 집합 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server를 지원 합니다 **iopenrowset:: Openrowset** 같은 제한 사항이 메서드:  
  
-   데이터베이스 ID(DBID) 구조체에 *pTableID* 매개 변수가 가리키는 기본 테이블 또는 뷰를 지정해야 합니다.  
  
-   DBID *eKind* 멤버는 DBKIND_NAME을 나타내야 합니다.  
  
-   DBID *uName* 멤버는 기존의 기본 테이블 또는 뷰 이름을 유니코드 문자열로 지정해야 합니다.  
  
-   **OpenRowset**의 *pIndexID* 매개 변수는 NULL이어야 합니다.  
  
 **IOpenRowset::OpenRowset**의 결과 집합에는 단일 행 집합이 들어 있습니다. 단일 행 집합을 포함하는 결과 집합은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 커서에서 지원될 수 있습니다. 커서 지원을 통해 개발자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 동시성 메커니즘을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
