---
title: CLR에서 LOB (Large Object) 매개 변수 처리 | Microsoft Docs
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
ms.openlocfilehash: 64b890f7b4dd801a43c85f0375987c6ff5f5cd1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081334"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>CLR의 LOB(Large Object) 매개 변수 처리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Sqlbytes** 및 **sqlbytes** 를 사용 하 여 lob (large object) 이진 유형 (**varbinary (max)**) 및 lob character type (**nvarchar (max)**) 매개 변수를 각각 전달 합니다. 이러한 형식을 사용하면 값 전체를 관리되는 공간에 복사하는 대신 데이터베이스의 LOB 값을 CLR(공용 언어 런타임) 루틴에 스트리밍할 수 있습니다. **SqlBinary** 및 **SqlString** 는 작은 이진 및 문자열 값에만 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
