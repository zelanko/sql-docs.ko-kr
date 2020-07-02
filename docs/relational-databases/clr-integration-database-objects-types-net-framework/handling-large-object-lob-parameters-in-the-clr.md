---
title: CLR에서 LOB (Large Object) 매개 변수 처리 | Microsoft Docs
description: 이 문서에서는 SQL Server CLR 통합의 매개 변수에 대 한 LOB (large object) 값을 처리 하는 방법을 설명 합니다. LOB 형식에 SqlBytes 및 Sqlbytes를 사용 합니다.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b10ac8c1ac9ccba804b892617df0b8d6c0d2f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637489"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>CLR의 LOB(Large Object) 매개 변수 처리
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Sqlbytes** 및 **sqlbytes** 를 사용 하 여 lob (large object) 이진 유형 (**varbinary (max)**) 및 lob character type (**nvarchar (max)**) 매개 변수를 각각 전달 합니다. 이러한 형식을 사용하면 값 전체를 관리되는 공간에 복사하는 대신 데이터베이스의 LOB 값을 CLR(공용 언어 런타임) 루틴에 스트리밍할 수 있습니다. **SqlBinary** 및 **SqlString** 는 작은 이진 및 문자열 값에만 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
