---
title: MSSQLSERVER_15404 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee32ea648fb80219052426e17e4e49d2a88dbe7a
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34317824"
---
# <a name="mssqlserver15404"></a>MSSQLSERVER_15404
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|15404|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_NTGRP_ERROR|  
|메시지 텍스트|Windows NT 그룹/사용자 '*user*'에 대한 정보를 가져올 수 없습니다. 오류 코드 *code*.|  
  
## <a name="explanation"></a>설명  
15404는 잘못된 보안 주체가 지정된 경우 인증에서 사용됩니다. 또는 Windows 계정의 가장은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정과 Windows 계정의 도메인 간에 완전 신뢰 관계가 없기 때문에 실패합니다.  
  
## <a name="user-action"></a>사용자 동작  
Windows 보안 주체가 존재하고 철자가 잘못되지 않았는지 확인합니다.  
  
이 오류가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 계정과 Windows 계정의 도메인 간에 완전 신뢰 관계가 없기 때문에 발생하는 경우 다음 작업 중 하나로 오류를 해결할 수 있습니다.  
  
-   Windows 사용자와 동일한 도메인에 있는 계정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스에 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 네트워크 서비스 또는 로컬 시스템과 같은 시스템 계정을 사용하는 경우 해당 컴퓨터가 Windows 사용자가 포함된 도메인에서 트러스트되어야 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용합니다.  
  
