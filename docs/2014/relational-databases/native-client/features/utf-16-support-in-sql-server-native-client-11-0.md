---
title: SQL Server Native Client 11.0의에서 utf-16 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205119"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0의 UTF-16 지원
  부터는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하 고는 `wchar` 종결 문자는 서로게이트 쌍의 상위 서로게이트 코드 포인트를 전과 경우 버퍼에 기록 된 문자 다음 `wchar` 문자가 하위 서로게이트 코드 포인트에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 상위 서로게이트 코드 포인트인 버퍼에 추가 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  
