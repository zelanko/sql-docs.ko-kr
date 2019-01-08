---
title: SQL 스크립트 생성(복제 개체) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2585452ee31c911ea6e288effc3e5e91fff88a64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800505"
---
# <a name="generate-sql-script-replication-objects"></a>SQL 스크립트 생성(복제 개체)
  복제 스크립트에는 게시 또는 구독과 같이 스크립팅된 복제 구성 요소를 구현하는 데 필요한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 시스템 저장 프로시저가 포함되어 있습니다. 토폴로지의 모든 복제 구성 요소는 재해 복구 계획의 일부로 스크립팅되어야 하며 반복 태스크를 자동화하는 데도 스크립트를 사용할 수 있습니다. 복제에서는 복제 개체를 스크립팅할 수 있는 다음 두 개의 대화 상자를 제공합니다.  
  
-   **SQL 스크립트 생성**대화 상자 - **msCoName** 의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]폴더 및 모든 하위 폴더의 상황에 맞는 메뉴에서 사용할 수 있습니다. 이 대화 상자를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 모든 복제 개체를 스크립팅할 수 있습니다.  
  
-   **SQL 스크립트 생성 \<ObjectName>** 은 게시 및 구독의 상황에 맞는 메뉴에서 사용할 수 있습니다. 이 대화 상자를 사용하여 개별 개체를 스크립팅할 수 있습니다.  
  
 이러한 대화 상자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 단일 인스턴스에 있는 개체를 스크립팅하며, 다른 인스턴스에 연결하여 관련 개체를 스크립팅하지는 않습니다.  
  
## <a name="generate-sql-script-options"></a>SQL 스크립트 생성 옵션  
 **배포자 속성**  
 저장 프로시저를 스크립팅하여 배포자를 설정 또는 해제하고, 배포자와 연결된 게시자를 추가 또는 삭제하고, 배포 데이터베이스를 생성 또는 삭제하려면 선택합니다.  
  
 **다음 데이터 원본의 게시**  
 저장 프로시저를 스크립팅하여 게시를 설정 또는 해제하고, 아티클, 밀어넣기 구독 및 복제 작업을 생성 또는 삭제하려면 선택합니다.  
  
 **다음 데이터 원본의 구독**  
 저장 프로시저를 스크립팅하여 끌어오기 구독 및 복제 작업을 생성 또는 삭제하려면 선택합니다.  
  
 **구성 요소 생성 또는 선택** 및 **구성 요소 삭제 또는 해제**  
 복제 개체를 생성 또는 삭제하는 명령을 스크립트에 포함할지 여부를 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 대화 상자를 사용하여 구성 요소를 설정 및 해제하는 스크립트 집합을 만들 것을 권장합니다.  
  
 **복제 작업**  
 저장 프로시저 호출과 함께 복제 작업을 스크립팅하려면 선택합니다. 이 옵션은 배포자에서 스크립팅하는 경우에만 사용할 수 있습니다.  
  
 복제 저장 프로시저는 실행될 때 필요한 작업을 만들기 때문에 이 옵션을 선택할 필요가 없습니다. 그러나 개별 작업을 다시 만들어야 하는 경우 작업 레코드를 만들어 두는 것이 좋습니다.  
  
## <a name="generate-sql-script-objectname-options"></a>SQL 스크립트 생성 \<ObjectName> 옵션  
 **구성 요소 생성 또는 선택** 및 **구성 요소 삭제 또는 해제**  
 복제 개체를 생성 또는 삭제하는 명령을 스크립트에 포함할지 여부를 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 대화 상자를 사용하여 구성 요소를 설정 및 해제하는 스크립트 집합을 만들 것을 권장합니다.  
  
 **복제 작업**  
 이 옵션은 **SQL 스크립트 생성** 대화 상자에서만 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 스크립팅](scripting-replication.md)  
  
  
