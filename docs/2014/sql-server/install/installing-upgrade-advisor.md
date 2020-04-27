---
title: 업그레이드 관리자 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f70d1cbb879f8fc91e48478fb820b71b51bfd2d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094320"
---
# <a name="installing-upgrade-advisor"></a>업그레이드 관리자 설치
  SQL Server 2014 업그레이드 관리자 설치 위치는 분석 대상에 따라 달라집니다. 업그레이드 관리자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 제외하고 모든 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 구성 요소의 원격 분석을 지원합니다. 인스턴스 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]를 검색 하지 않는 경우에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결할 수 있고 [업그레이드 관리자의 필수 구성 요소](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)를 충족 하는 모든 컴퓨터에 업그레이드 관리자를 설치할 수 있습니다. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]의 인스턴스를 검색하는 경우에는 보고서 서버에 업그레이드 관리자를 설치해야 합니다.  
  
 **Sqlua .msi** 파일을 실행 하 여 업그레이드 관리자를 설치 합니다. 명령 프롬프트를 사용하여 무인 및 자동 설치를 수행할 수 있습니다. 구문 및 예제 [는 명령 프롬프트에서 업그레이드 관리자 설치를](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) 참조 하세요.  
  
 SQLUA.msi를  
  
-   제품 미디어의 redist 폴더에 있습니다. **redist** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [SQL 2014 기능 팩 다운로드](https://www.microsoft.com/download/details.aspx?id=42295)의 일부로 다운로드 합니다.  
  
## <a name="uninstalling-upgrade-advisor"></a>업그레이드 관리자 제거  
 **프로그램 추가/제거**를 사용 하 여 업그레이드 관리자를 제거할 수 있습니다. 명령 프롬프트 구문도 제거/설치 제거를 지원합니다.  
  
  
