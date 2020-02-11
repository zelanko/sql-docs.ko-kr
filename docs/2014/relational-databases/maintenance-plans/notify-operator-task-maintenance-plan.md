---
title: 운영자에게 알림 태스크(유지 관리 계획) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.notifyoperator.f1
helpviewer_keywords:
- Notify Operator Task dialog box
ms.assetid: 39c0797c-ad2b-4591-85c9-a23a7f902895
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ef94ed9e296c588b70789ace0bbbbe79bc8008f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205960"
---
# <a name="notify-operator-task-maintenance-plan"></a>운영자에게 알림 태스크(유지 관리 계획)
  운영자에 **게 알림 태스크** 대화 상자를 사용 하 여이 유지 관리 계획에 자동 알림을 추가할 수 있습니다. 이 태스크를 사용 하려면 MSDB를 메일 호스트 데이터베이스로 사용 하도록 설정 하 고 올바르게 구성 해야 하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 유효한 전자 메일 주소를 포함 하는 에이전트 운영자가 데이터베이스 메일 있어야 합니다.  
  
 이 태스크에서는 sp_notify_operator 저장 프로시저를 사용합니다.  
  
## <a name="options"></a>옵션  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **알릴 운영자**  
 전자 메일의 받는 사람을 지정합니다.  
  
 **알림 메시지 제목**  
 알림 메시지 제목 줄에 포함할 텍스트를 지정합니다.  
  
 **알림 메시지 본문**  
 알림 메시지 본문에 포함할 텍스트를 지정합니다.  
  
 **T-sql 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows 통합 보안 사용**  
 Windows 인증 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 을 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인스턴스에 연결 합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../database-mail/database-mail.md)   
 [Transact-sql&#41;sp_notify_operator &#40;](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)  
  
  
