---
description: 구독자 속성
title: 구독자 속성 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.subscribers.f1
helpviewer_keywords:
- Subscriber Properties dialog box
ms.assetid: 32aa0347-64e4-4aa4-ac57-6bd3e5d52070
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: b2bd65605a719408ac08454584601cb5636faa4a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479634"
---
# <a name="subscriber-properties"></a>구독자 속성
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  **구독자 속성** 대화 상자에는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행 중인 구독자와 관련된 정보가 포함되어 있습니다.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]

  
## <a name="options"></a>옵션  
 **에이전트에서 구독자 연결**  
 배포 에이전트 및 병합 에이전트가 배포자에서 구독자로 연결하는 컨텍스트로서, [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이전 버전에만 적용됩니다.  
  
 **에이전트 프로세스 계정 가장** 을 선택하여 배포자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 계정의 컨텍스트를 사용하여 구독자에 연결하거나 **SQL Server 인증** 을 지정한 다음 **로그인** 및 **암호** 에 값을 입력합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 **에이전트 프로세스 계정 가장** 을 선택할 것을 권장합니다.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 경우 연결 정보는 새 구독 마법사에서 각 구독에 대해 지정되며 **구독 속성** 대화 상자에서 변경할 수 있습니다.  
  
 **기본 에이전트 일정**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]를 실행 중인 구독자에 대해 새 구독 마법사에서 사용하는 기본 일정입니다.  
  
 **기타**  
 구독자 및 구독자 유형에 대한 정보를 포함합니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
