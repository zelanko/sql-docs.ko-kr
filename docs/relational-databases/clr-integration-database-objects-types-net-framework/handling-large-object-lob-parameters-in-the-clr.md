---
title: CLR에서 큰 개체(LOB) 매개 변수 처리 | 마이크로 소프트 문서
description: 이 문서에서는 SQL Server CLR 통합에서 매개 변수에 대한 큰 개체(LOB) 값을 처리하는 방법을 설명합니다. LOB 형식에 SqlBytes 및 SqlChars를 사용합니다.
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
ms.openlocfilehash: 0941ca2f5fc1a05397dd3dbec5e0dd27c6e5d815
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488462"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>CLR의 LOB(Large Object) 매개 변수 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SqlBytes** 및 **SqlChars를** 사용하여 큰 개체(LOB) 바이너리 형식(varbinary(최대) 및 LOB 문자 유형(nvarchar(최대)) 매개 변수를 각각 전달합니다.**varbinary(max)****nvarchar(max)** 이러한 형식을 사용하면 값 전체를 관리되는 공간에 복사하는 대신 데이터베이스의 LOB 값을 CLR(공용 언어 런타임) 루틴에 스트리밍할 수 있습니다. **SqlBinary** 및 **SqlString작은** 이진 및 문자 문자열 값에만 사용 되어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
