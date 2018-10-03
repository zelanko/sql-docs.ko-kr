---
title: Data Migration Assistant를 사용 하 여 SQL Server 로그인 마이그레이션 | Microsoft Docs
description: Data Migration Assistant를 사용 하 여 SQL Server 로그인을 마이그레이션하는 방법을 알아봅니다
ms.custom: ''
ms.date: 08/29/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: e52fdcd55cddea31e317afe04833f5413c006325
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836941"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 SQL Server 로그인 마이그레이션

이 문서에서는 Data Migration Assistant를 사용 하 여 SQL Server 로그인 마이그레이션 개요를 제공 합니다. 

## <a name="which-logins-are-migrated"></a>로그인은 마이그레이션되지

- Windows 보안 주체 (예: 도메인 사용자 또는 Windows 도메인 그룹)에 따라 로그인을 마이그레이션할 수 있습니다. 또한 SQL Server 로그인이 라고도 하는 SQL 인증을 기반으로 작성 하는 로그인을 마이그레이션할 수 있습니다.

- Data Migration Assistant 현재 지원 하지 않습니다 자격 증명에 매핑된 로그인을 독립형 보안 인증서 (인증서에 매핑된 로그인)을 독립형 비대칭 키 (비대칭 키에 매핑된 로그인)와 연결 된 로그인.

- Data Migration Assistant를 이동 하지 않는 합니다 **sa** 로 이중 해시 표시 이름의 로그인 및 서버가 원칙 (\#\#), 내부 에서만 사용 되는 합니다.

- 기본적으로 Data Migration Assistant 선택 마이그레이션할 모든 정규화 된 로그인 합니다. 필요에 따라 특정 로그인 마이그레이션하도록 선택할 수 있습니다. Data Migration Assistant 마이그레이션하면 모든 정규화 된 로그인, 사용자 로그인 매핑을 마이그레이션되는 데이터베이스에 그대로 유지 됩니다. 

  특정 로그인을 마이그레이션하려는 경우에 마이그레이션을 위해 선택한 데이터베이스에서 하나 이상의 사용자에 매핑되는 로그인을 선택 해야 합니다.

- 로그인 마이그레이션의 일부로 Data Migration Assistant도 사용자 정의 서버 역할을 이동 하 고 사용자 정의 서버 역할에 서버 수준 사용 권한을 추가 합니다. 역할의 소유자에 설정할 **sa** 보안 주체입니다.

## <a name="during-and-after-migration"></a>도중과 마이그레이션 후

- 로그인 마이그레이션의 일부로 Data Migration Assistant는 권한을 할당 대상 SQL Server에서 보안 개체에 원본 SQL Server에 있는 합니다. 

  로그인에 이미 있는 경우 대상 SQL Server, Data Migration Assistant 보안 개체에 할당 된 사용 권한만 마이그레이션되고 다시 전체 로그인을 만들지 않습니다.

- Data Migration Assistant를 가장 하기 위해 노력 로그인이 대상 서버에 이미 있는 경우 데이터베이스 사용자에 게 해당 로그인에 매핑합니다.

- 로그인 마이그레이션 및 권장 되는 마이그레이션 후 작업의 전반적인 상태를 이해 하는 마이그레이션 결과 검토 하는 것이 좋습니다.

## <a name="resources"></a>리소스

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
