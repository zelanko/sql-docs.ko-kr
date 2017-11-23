---
title: "CLR의 LOB (Large Object) 매개 변수 처리 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fea5bc671483adbc29af49e1b88ed56156fb429f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>CLR의 LOB(Large Object) 매개 변수 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용 하 여 **SqlBytes** 및 **SqlChars** (large object) 이진 형식을 전달할 (**varbinary (max)**) 및 LOB 문자 형식 (**nvarchar (max)**) 매개 변수를 각각. 이러한 형식을 사용하면 값 전체를 관리되는 공간에 복사하는 대신 데이터베이스의 LOB 값을 CLR(공용 언어 런타임) 루틴에 스트리밍할 수 있습니다. **SqlBinary** 및 **SqlString** 작은 이진 및 문자열 값에 대해서만 사용 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
