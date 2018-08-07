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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: dad6b0cf5b81674cacf35f816e934fce95930621
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535493"
---
# <a name="implementing-an-outer-join"></a>외부 조인 구현
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 고유하게 컴파일된 T-SQL 모듈에서 LEFT 및 RIGHT OUTER JOIN이 지원됩니다.  
  
  
