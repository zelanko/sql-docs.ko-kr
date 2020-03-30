---
title: 로그 전달 모니터 설정 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: 216fb75c9dcdffc83e8f4f21469aaa9cfc1b11d8
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67934411"
---
# <a name="log-shipping-monitor-settings"></a>로그 전달 모니터 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 페이지를 사용하여 로그 전달 모니터 서버의 속성을 구성하고 수정할 수 있습니다.  
  
 로그 전달 개념에 대한 설명은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **모니터 서버 인스턴스**  
 로그 전달 구성을 위한 모니터 서버로 현재 구성되어 있는 서버 인스턴스의 이름을 표시합니다.  
  
 **연결**  
 모니터 서버로 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 선택하여 연결합니다. 연결 시 사용한 계정은 보조 서버 인스턴스에서 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
 **작업의 프록시 계정 가장**  
 로그 전달에서 모니터 서버 인스턴스에 연결할 때 SQL Server 에이전트 프록시 계정을 가장합니다. 백업, 복사 및 복구 프로세스에서 모니터 서버에 연결하여 로그 전달 작업 상태를 업데이트할 수 있어야 합니다.  
  
 **다음 SQL Server 로그인 사용**  
 로그 전달에서 모니터 서버 인스턴스에 연결할 때 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용할 수 있습니다. 백업, 복사 및 복구 프로세스에서 모니터 서버에 연결하여 로그 전달 작업 상태를 업데이트할 수 있어야 합니다. 로그 전달에서 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 사용하려면 이 옵션을 선택한 다음 로그인과 암호를 지정합니다.  
  
 **다음 기간 이후에 기록 삭제**  
 로그 전달 기록 정보를 삭제하기 전에 모니터 서버에서 보관하는 기간을 지정합니다.  
  
 **작업 이름**  
 백업 또는 복원 임계값이 초과될 때 로그 전달에서 경고를 발생시키는 데 사용되는 SQL Server 에이전트 경고 작업의 이름을 나타냅니다. 처음 이 작업을 만들 때 입력란에 이름을 입력하여 변경할 수 있습니다.  
  
 **일정**  
 SQL Server 에이전트 경고 작업의 현재 일정을 나타냅니다.  
  
 **편집**  
 SQL Server 에이전트 경고 작업 매개 변수를 수정합니다.  
  
 **이 작업 비활성화**  
 SQL Server 에이전트 경고 작업을 일시 중지합니다.  
  
  
