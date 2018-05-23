---
title: 외부 조인 구현 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 67084043-6b23-4975-b9db-6e49923d4bab
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4b525e77bbccd8539e40c755b4427b0110028137
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="implementing-an-outer-join"></a>외부 조인 구현
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 고유하게 컴파일된 T-SQL 모듈에서 LEFT 및 RIGHT OUTER JOIN이 지원됩니다.  
  
  
