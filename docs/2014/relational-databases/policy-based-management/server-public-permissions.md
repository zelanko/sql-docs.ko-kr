---
title: 서버 public 사용 권한 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7913c4715f47b8105b72b1c817dbe77e52d40539
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066705"
---
# <a name="server-public-permissions"></a>서버 public 사용 권한
  이 규칙은 public 서버 역할에 서버 사용 권한이 있는지 확인합니다. 서버에 만들어진 모든 로그인은 public 서버 역할의 멤버입니다. 이 조건이 충족될 경우 서버의 모든 로그인은 서버 사용 권한을 갖습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 서버 public 역할에 서버 사용 권한을 부여하지 마십시오.  
  
> [!IMPORTANT]  
>  설치가 완료 되 면 **PUBLIC** 역할에는 `CONNECT` **관리자 전용 연결**을 제외한 모든 끝점에 대 한 권한이 있습니다. 이것은 정상이며 일반적으로 변경할 수 없습니다. 새 로그인을 만들 때 자동으로 부여되는 `CONNECT SQL` 권한으로 액세스가 제어됩니다.  
  
### <a name="for-more-information"></a>참조 항목  
 [SQL Server 보안 설정](../security/securing-sql-server.md)  
  
  
