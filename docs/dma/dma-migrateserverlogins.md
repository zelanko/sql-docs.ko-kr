---
title: Data Migration Assistant를 사용 하 여 SQL Server 로그인 마이그레이션
description: Data Migration Assistant를 사용 하 여 SQL Server 로그인을 마이그레이션하는 방법을 알아봅니다.
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: f721800de13d11eefa1cabdd2f23fda838db9396
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82885790"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Data Migration Assistant를 사용 하 여 SQL Server 로그인 마이그레이션

이 문서에서는 Data Migration Assistant를 사용 하 여 SQL Server 로그인을 마이그레이션하는 개요를 제공 합니다.

> [!IMPORTANT]
> 이 항목은 이후 버전의 온-프레미스 제품으로 업그레이드 하거나 Azure Virtual Machines에서 SQL Server 하는 SQL Server 관련 된 시나리오에 적용 됩니다.

## <a name="which-logins-are-migrated"></a>마이그레이션되는 로그인

- Windows 보안 주체 (예: 도메인 사용자 또는 Windows 도메인 그룹)를 기반으로 하 여 로그인을 마이그레이션할 수 있습니다. 또한 로그인 SQL Server 라고도 하는 SQL 인증을 기반으로 만든 로그인을 마이그레이션할 수 있습니다.

- Data Migration Assistant는 현재 독립 실행형 보안 인증서 (인증서에 매핑된 로그인), 독립 실행형 비대칭 키 (비대칭 키에 매핑된 로그인) 및 자격 증명에 매핑된 로그인과 연결 된 로그인을 지원 하지 않습니다.

- Data Migration Assistant **sa** 로그인 및 서버 원칙은 \# \# 내부용 으로만 사용 되는 이중 해시 표시 ()로 묶인 이름으로 이동 하지 않습니다.

- 기본적으로 Data Migration Assistant는 마이그레이션할 모든 정규화 된 로그인을 선택 합니다. 선택적으로 마이그레이션할 특정 로그인을 선택할 수 있습니다. Data Migration Assistant에서 모든 정규화 된 로그인을 마이그레이션하면 로그인 사용자 매핑이 마이그레이션되는 데이터베이스에 그대로 유지 됩니다.

  특정 로그인을 마이그레이션할 계획인 경우 마이그레이션을 위해 선택한 데이터베이스에서 하나 이상의 사용자에 게 매핑된 로그인을 선택 해야 합니다.

- 로그인 마이그레이션의 일부로 Data Migration Assistant 사용자 정의 서버 역할을 이동 하 고 사용자 정의 서버 역할에 서버 수준 사용 권한을 추가 합니다. 역할의 소유자는 **sa** 보안 주체로 설정 됩니다.

## <a name="during-and-after-migration"></a>마이그레이션 중 및 이후

- 로그인 마이그레이션의 일부로 Data Migration Assistant 원본 SQL Server에 존재 하는 대상 SQL Server에 대 한 사용 권한을 보안 개체에 할당 합니다.

  로그인이 대상 SQL Server에 이미 있는 경우에는 Data Migration Assistant 보안 개체에 할당 된 사용 권한만 마이그레이션하고 전체 로그인을 다시 만들지 않습니다.

- 로그인이 대상 서버에 이미 있는 경우에는 로그인을 데이터베이스 사용자에 게 매핑하기 위해 Data Migration Assistant 합니다.

- 마이그레이션 결과를 검토 하 여 로그인 마이그레이션의 전반적인 상태 및 권장 되는 마이그레이션 후 작업을 이해 하는 것이 좋습니다.

## <a name="resources"></a>리소스

[Data Migration Assistant(DMA)](../dma/dma-overview.md)

[Data Migration Assistant: 구성 설정](../dma/dma-configurationsettings.md)
