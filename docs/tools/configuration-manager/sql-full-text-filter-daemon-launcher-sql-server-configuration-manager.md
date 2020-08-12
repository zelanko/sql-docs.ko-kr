---
title: SQL 전체 텍스트 필터 데몬 시작 관리자(SQL Server 구성 관리자)
description: SQL Server에서 전체 텍스트 검색에 필요한 프로세스를 시작하는 데 사용하는 서비스인 SQL 전체 텍스트 필터 데몬 시작 관리자에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d0dc03db-5f76-4558-b041-1ac7b9b5bb16
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 63a3cb64254f314d8f997f0b062629c09b1eec39
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881874"
---
# <a name="sql-full-text-filter-daemon-launcher-sql-server-configuration-manager"></a>SQL 전체 텍스트 필터 데몬 시작 관리자(SQL Server 구성 관리자)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체 텍스트 검색에서 전체 텍스트 검색 필터링 및 단어 분리를 처리하는 필터 데몬 호스트 프로세스를 시작하기 위해 SQL 전체 텍스트 필터 데몬 시작 관리자(FDHOST Launcher) 서비스가 사용됩니다. 전체 텍스트 검색을 사용하려면 이 서비스를 실행해야 합니다. FDHOST Launcher 서비스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 특정 인스턴스와 연결된 인스턴스 인식형 서비스입니다. FDHOST Launcher 서비스는 시작된 각 필터 데몬 호스트 프로세스로 서비스 계정 정보를 전파합니다. 필터 데몬 호스트 프로세스에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "전체 텍스트 검색 아키텍처"를 참조하십시오.  
  
  
