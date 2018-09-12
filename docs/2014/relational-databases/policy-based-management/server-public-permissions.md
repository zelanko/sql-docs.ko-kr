---
title: 서버 public 사용 권한 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 9a276caa-ea38-473d-92bc-26302bfcf660
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1389d712ff00438a2e6251315e8ebcc55e7fbff2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43813919"
---
# <a name="server-public-permissions"></a>서버 public 사용 권한
  이 규칙은 public 서버 역할에 서버 사용 권한이 있는지 확인합니다. 서버에 만들어진 모든 로그인은 public 서버 역할의 멤버입니다. 이 조건이 충족될 경우 서버의 모든 로그인은 서버 사용 권한을 갖습니다.  
  
## <a name="best-practices-recommendations"></a>최선의 구현 방법 권장 사항  
 서버 public 역할에 서버 사용 권한을 부여하지 마십시오.  
  
> [!IMPORTANT]  
>  설치가 완료 된 후 합니다 **공용** 역할에 `CONNECT` 를 제외한 모든 끝점에 대 한 권한이 합니다 **관리자 전용 연결**합니다. 이것은 정상이며 일반적으로 변경할 수 없습니다. (사용 하 여 액세스 제어를 `CONNECT SQL` 새 로그인을 만들 때 자동으로 부여 된 권한입니다.)  
  
### <a name="for-more-information"></a>참조 항목  
 [SQL Server 보안 설정](../security/securing-sql-server.md)  
  
  
