---
title: "명명 된 파이프 속성 (프로토콜 탭)을 클라이언트 프로토콜-| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 33d801033e2431f465e97502dcabf37f6a9c4847
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# 클라이언트 프로토콜 - 명명된 파이프 속성(프로토콜 탭)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **명명된 파이프 속성** 대화 상자의 **프로토콜** 탭을 사용하여 기본 파이프에 대한 설명을 확인하거나 수정할 수 있습니다. 다른 파이프에 연결하려면 **기본 파이프** 상자에 해당 파이프를 입력합니다. 연결 문자열에 대한 자세한 내용은 [Creating a Valid Connection String Using Named Pipes](http://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)을 참조하십시오.  
  
## 옵션  
 **기본 파이프**  
 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결할 때 명명된 파이프 Net-library가 사용할 기본 파이프를 지정합니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 수신 대기 합니다.`\\.\pipe\sql\query`  
  
 기본 파이프에 연결하려면 `sql\query`  
  
 **설정**  
 가능한 값은 **예** 및 **아니요**입니다.  
  
## 관련 항목:  
 [네트워크 프로토콜 선택](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  

