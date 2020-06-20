---
title: SQL Server Native Client 11.0의 UTF-16 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: rothja
ms.author: jroth
ms.openlocfilehash: af8581071400db888fb508b88f8e8ae93bc71f70
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039004"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0의 UTF-16 지원
  부터는 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공 하 고, `wchar` 종료 문자 이전에 버퍼에 작성 된 문자가 서로게이트 쌍의 상위 서로게이트 코드 지점이 며, 다음 `wchar` 문자가 하위 서로게이트 코드 포인트 이면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client는 상위 서로게이트 코드 포인트를 버퍼에 추가 하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)  
  
  
