---
title: "SQL 전체 텍스트 필터 데몬 시작 관리자 (SQL Server 구성 관리자) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 123cbf16970be0820dbda43b0eb51a5e1bca4852
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 전체 텍스트 필터 데몬 시작 관리자(SQL Server 구성 관리자)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색에서 전체 텍스트 검색 필터링 및 단어 분리를 처리하는 필터 데몬 호스트 프로세스를 시작하기 위해 SQL 전체 텍스트 필터 데몬 시작 관리자(FDHOST Launcher) 서비스가 사용됩니다. 전체 텍스트 검색을 사용하려면 이 서비스를 실행해야 합니다. FDHOST Launcher 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스와 연결된 인스턴스 인식형 서비스입니다. FDHOST Launcher 서비스는 시작된 각 필터 데몬 호스트 프로세스로 서비스 계정 정보를 전파합니다. 필터 디먼 호스트 프로세스에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "전체 텍스트 검색 아키텍처"를 참조하세요.  
  
  
