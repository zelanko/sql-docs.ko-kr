---
title: SQL Server 로그인 (데이터 마이그레이션 길잡이)를 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5d3347eb2aff8e14c3938880dde6fe1879eb910d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="migrating-sql-server-logins-using-data-migration-assistant"></a>데이터 마이그레이션 길잡이 사용 하 여 마이그레이션 SQL Server 로그인

이 문서에서는 데이터 Migration Assistant를 사용 하 여 마이그레이션 SQL Server 로그인에 대 한 개요를 제공 합니다. 

## <a name="key-concepts"></a>주요 개념
주요 개념은 다음과 같습니다.

- Windows 보안 주체 (예: 도메인 사용자 또는 Windows 도메인 그룹)에 따라 로그인을 마이그레이션할 수 있습니다. 또한 SQL 인증을 SQL Server 로그인 함에 따라 생성 된 로그인을 마이그레이션할 수 있습니다.

- 데이터 마이그레이션 길잡이 현재 지원 하지 않습니다. 자격 증명에 매핑된 로그인을 독립형 보안 인증서 (인증서에 매핑된 로그인), 독립형 비대칭 키 (비대칭 키에 매핑된 로그인)와 연결 된 로그인

- 데이터 마이그레이션 길잡이 이동 하지 않습니다는 **sa** 이름이 이중 해시 표시로 묶인 로그인 및 서버 원칙 (\#\#), 내부에 사용에 대 한 합니다.

- 기본적으로 데이터 마이그레이션 Assistatn 마이그레이션할 정규화 된 모든 로그인을 선택 합니다. 필요에 따라 마이그레이션할 특정 로그인을 선택할 수 있습니다. 데이터 마이그레이션 길잡이 마이그레이션하면 모든 정규화 된 로그인, 사용자 로그인 매핑을 마이그레이션되는 데이터베이스에 그대로 유지 됩니다. 

  특정 로그인 마이그레이션하려는 경우에 마이그레이션을 위해 선택한 데이터베이스에 하나 이상의 사용자에 매핑되는 로그인을 선택 해야 합니다.

- 로그인 마이그레이션의 일부로 데이터 Migration Assistant도 사용자 정의 서버 역할 이동 하 고 사용자 정의 서버 역할에 서버 수준 사용 권한을 추가 합니다. 역할의 소유자를로 설정 됩니다 **sa** 보안 주체입니다.

- 로그인 마이그레이션의 일부로 데이터 Migration Assistant 사용 권한을 대상 SQL Server에서 보안 개체를 할당 원본 SQL Server에 있는 됩니다. 

  SQL Server 대상에 이미 로그인 한 경우 데이터 Migration Assistant 보안 개체에 할당 된 권한만 마이그레이션되고 전체 로그인을 다시 만들어지지 않습니다.

- 데이터 마이그레이션 길잡이 하면 최상의 노력 로그인이 대상 서버에 이미 있는 경우 데이터베이스 사용자에 게 로그인을 매핑할 수 있습니다.

- 로그인 마이그레이션 및 마이그레이션 후 권장된 조치의 전반적인 상태를 이해 하는 마이그레이션 결과 검토 하는 것이 좋습니다.

## <a name="resources"></a>리소스

[데이터 마이그레이션 길잡이 (DMA)](../dma/dma-overview.md)

[데이터 마이그레이션 길잡이: 구성 설정](../dma/dma-configurationsettings.md)
