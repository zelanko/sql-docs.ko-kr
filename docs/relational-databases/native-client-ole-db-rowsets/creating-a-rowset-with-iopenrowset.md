---
description: IOpenRowset (Native Client OLE DB 공급자)를 사용 하 여 행 집합 만들기
title: IOpenRowset (Native Client OLE DB 공급자)를 사용 하 여 행 집합 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b6d6d554c6ac0335ec0504886ea7e8de06437f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499144"
---
# <a name="creating-a-rowset-with-iopenrowset-in-sql-server-native-client"></a>SQL Server Native Client에서 IOpenRowset을 사용 하 여 행 집합 만들기
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 다음과 같은 제한 사항이 있는 **iopenrowset:: OpenRowset** 메서드를 지원 합니다.  
  
-   데이터베이스 ID(DBID) 구조체에 *pTableID* 매개 변수가 가리키는 기본 테이블 또는 뷰를 지정해야 합니다.  
  
-   DBID *eKind* 멤버는 DBKIND_NAME을 나타내야 합니다.  
  
-   DBID *uName* 멤버는 기존의 기본 테이블 또는 뷰 이름을 유니코드 문자열로 지정해야 합니다.  
  
-   **OpenRowset**의 *pIndexID* 매개 변수는 NULL이어야 합니다.  
  
 **IOpenRowset::OpenRowset**의 결과 집합에는 단일 행 집합이 들어 있습니다. 단일 행 집합을 포함하는 결과 집합은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 커서에서 지원될 수 있습니다. 커서 지원을 통해 개발자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 동시성 메커니즘을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [행 집합](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
