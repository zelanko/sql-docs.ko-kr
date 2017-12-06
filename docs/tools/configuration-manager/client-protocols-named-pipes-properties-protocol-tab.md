---
title: "명명 된 파이프 속성 (프로토콜 탭)을 클라이언트 프로토콜-| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c5c868a2051f1eb8dbdc59bd3b1247454292baf
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>클라이언트 프로토콜 - 명명된 파이프 속성(프로토콜 탭)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 하 여 Configuration Manager는 **프로토콜** 탭에 **명명 된 파이프 속성** 대화 상자를 보거나 기본 파이프에 대 한 설명을 수정 합니다. 다른 파이프에 연결하려면 **기본 파이프** 상자에 해당 파이프를 입력합니다. 연결 문자열에 대한 자세한 내용은 [Creating a Valid Connection String Using Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)을 참조하십시오.  
  
## <a name="options"></a>옵션  
 **기본 파이프**  
 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때 명명된 파이프 Net-library가 사용할 기본 파이프를 지정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 `\\.\pipe\sql\query`  
  
 기본 파이프에 연결하려면 `sql\query`  
  
 **설정**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
## <a name="see-also"></a>관련 항목:  
 [네트워크 프로토콜 선택](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
