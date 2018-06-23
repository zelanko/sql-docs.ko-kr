---
title: SQL Server Native Client 11.0의에서 utf-16 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66198f42676944967a2d655f14a27470922fd318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36183242"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0의 UTF-16 지원
  부터는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하 고 경우는 `wchar` 종결 문자는 서로게이트 쌍의 상위 서로게이트 코드 포인트 전과 경우 버퍼에 기록 된 문자 다음 `wchar` 문자 하위 서로게이트 코드 포인트는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 상위 서로게이트 코드 포인트 버퍼에 추가 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  