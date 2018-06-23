---
title: 격리 수준 (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1870c4f9f348c9d1b2ca52b94ee38a3e5d38190
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698074"
---
# <a name="isolation-levels-ole-db"></a>격리 수준(OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트는 연결에 대한 트랜잭션 격리 수준을 제어할 수 있습니다. 트랜잭션 격리 수준을 제어 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 사용:  
  
-   DBPROPSET_SESSION 속성인 DBPROP_SESS_AUTOCOMMITISOLEVELS에 대 한는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 기본 자동 커밋 모드입니다.  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 수준에 대해 Native Client OLE DB 공급자 기본값은 DBPROPVAL_TI_READCOMMITTED입니다.  
  
-   *isoLevel* 의 매개 변수는 **itransactionlocal:: Starttransaction** 로컬 수동 커밋 트랜잭션에 대 한 메서드.  
  
-   *isoLevel* 의 매개 변수는 **itransactiondispenser:: Begintransaction** 방법을 MS DTC 통합 분산 트랜잭션을 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 사용하면 커밋되지 않은 읽기 격리 수준에서 읽기 전용으로 액세스할 수 있습니다. 이외의 다른 모든 수준은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체에 잠금을 적용하므로 동시성을 제한합니다. 클라이언트에 더 높은 동시성 수준이 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터 동시 액세스에 대해 더 높은 수준의 제한을 적용합니다. 가장 높은 수준의 데이터에 대 한 동시 액세스를 유지 관리 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자 특정 동시성 수준에 대 한 해당 요청을 지능적으로 제어 해야 합니다.  
  
> [!NOTE]  
>  스냅숏 격리 수준은 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입되었습니다. 자세한 내용은 참조 [스냅숏 격리 작업](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [의](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
