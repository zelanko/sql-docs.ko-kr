---
title: 업그레이드 관리자 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
caps.latest.revision: 34
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a8c15c361f1fc29a805948b3761fd0a04c5c396c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37327013"
---
# <a name="installing-upgrade-advisor"></a>업그레이드 관리자 설치
  SQL Server 2014 업그레이드 관리자 설치 위치는 분석 대상에 따라 달라집니다. 업그레이드 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외하고 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 원격 분석을 지원합니다. 인스턴스를 검색 하지 않는 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에 연결할 수 있는 모든 컴퓨터에 업그레이드 관리자를 설치할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 충족 하는 합니다 [업그레이드 관리자 필수 구성 요소](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)합니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인스턴스를 검색하는 경우에는 보고서 서버에 업그레이드 관리자를 설치해야 합니다.  
  
 실행 합니다 **SQLUA.msi** 업그레이드 관리자를 설치 하는 파일입니다. 명령 프롬프트를 사용하여 무인 및 자동 설치를 수행할 수 있습니다. 참조 [명령 프롬프트에서 업그레이드 관리자 설치](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) 구문 및 예제에 대 한 합니다.  
  
 SQLUA.msi를    
  
-   에 **redist** 의 폴더를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 미디어입니다.  
  
-   일부로 합니다 [SQL 2014 기능 팩 다운로드](http://www.microsoft.com/download/details.aspx?id=42295)합니다.  
  
## <a name="uninstalling-upgrade-advisor"></a>업그레이드 관리자 제거  
 사용 하 여 업그레이드 관리자를 제거할 수 있습니다 **프로그램 추가 / 제거**합니다. 명령 프롬프트 구문도 제거/설치 제거를 지원합니다.  
  
  
