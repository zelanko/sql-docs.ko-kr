---
title: 사용 중인 파일 검사 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ccd65867-d4c0-43b2-8361-7fd41c6f79ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c18860cf43c31096b984d45b18fba7828de6ea90
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48065663"
---
# <a name="check-files-in-use"></a>사용 중인 파일 확인
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 설치한 후 Windows가 다시 시작되지 않도록 하려면 사용 중인 파일 검사 페이지에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트 설치 프로그램에 필요한 파일을 사용 중인 프로세스를 확인합니다.  
  
 업데이트할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결된 응용 프로그램 및 서비스를 모두 중지합니다. 이때 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 와 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]도 중지해야 합니다.  
  
 설치 중에 잠겨 있는 파일이 발견되면 설치가 끝난 후 컴퓨터를 다시 시작해야 할 수 있습니다. 필요한 경우 컴퓨터를 다시 시작하라는 메시지가 표시됩니다. 설치 프로그램에서 설치를 진행하는 동안 특정 서비스를 중지해야 했으면 설치를 마친 후 해당 서비스가 다시 시작됩니다.  
  
 설치 후 컴퓨터를 다시 시작하지 않아도 되도록 하기 위해 파일을 사용 중인 프로세스의 목록이 설치 프로그램을 통해 표시됩니다. 목록에 나와 있는 프로세스와 응용 프로그램을 중지하거나 종료합니다. 그런 다음 **검사 새로 고침** 을 클릭하여 검사를 다시 실행합니다. 실행 중인 검사를 끝내려면 **검사 중지** 를 클릭합니다. 잠겨 있는 파일이 없으면 테이블에 아무 것도 표시되지 않습니다. 잠긴 프로세스를 모두 닫거나 중지했으면 **다음** 을 클릭하여 작업을 계속 진행합니다.  
  
 설치 과정에서 로그 파일에 정보가 기록됩니다. 로그 파일을 보는 방법은 [SQL Server 설치 로그 파일 보기 및 읽기](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) 및 [방법: SQL Server 설치 로그 파일 읽기](http://go.microsoft.com/fwlink/?LinkID=134490)를 참조하세요.  
  
 로그 파일에는 다음 정보가 포함됩니다.  
  
-   프로세스 이름  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기능 이름  
  
-   프로세스 유형  
  
-   프로세스를 실행하는 데 사용된 계정  
  
-   프로세스 ID  
  
-   잠겨 있는 파일 이름  
  
## <a name="uielement-list"></a>UIElement 목록  
  
|이름|Description|  
|----------|-----------------|  
|처리|업데이트해야 할 파일을 사용하고 있는 프로세스의 전체 이름을 표시합니다.|  
|형식|프로세스의 유형을 표시합니다.|  
|계정|프로세스를 실행하는 데 사용된 계정을 표시합니다.|  
|프로세스 ID|프로세스 ID를 표시합니다.|  
  
  
