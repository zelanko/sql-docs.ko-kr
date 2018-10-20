---
title: SQL Server Machine Learning Services에 대 한 방화벽 구성 | Microsoft Docs
description: SQL Server Machine Learning Services에 대 한 방화벽을 구성 하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: d2bf36ea9a7c7a0b193dc4613f6a36f58e66014a
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419058"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 방화벽 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 관리자나 설계자 명심 해야 machine learning 서비스를 사용 하는 경우 방화벽 구성 고려 사항을 나열 합니다.

## <a name="default-firewall-rules"></a>기본 방화벽 규칙

기본적으로 SQL Server 설치 프로그램을 방화벽 규칙을 만들어 아웃 바운드 연결을 해제 합니다.

SQL Server 2016 및 2017에서는 이러한 규칙이 설치에 대 한 아웃 바운드 규칙이 만들어진 로컬 사용자 계정에 기반한 **SQLRUserGroup** 해당 멤버에 대 한 네트워크 액세스를 거부 하는 (각 작업자 계정으로 제시 된 로컬 원칙 적용 규칙입니다. SQLRUserGroup에 대 한 자세한 내용은 참조 하세요. [SQL Server Machine Learning Services의 확장성 프레임 워크에 대 한 보안 개요](../../advanced-analytics/concepts/security.md#sqlrusergroup)합니다.

SQL Server 2019 AppContainers, 이동의 일부로 가지 AppContainer Sid에 따라 새 방화벽 규칙: SQL Server 설치 프로그램을 만들어 각각 20 AppContainers에 대 한 합니다. 방화벽 규칙 이름에 대 한 명명 규칙이 **SQL Server 인스턴스 MSSQLSERVER의에서 AppContainer 00에 대 한 네트워크 액세스를 차단**, 여기서 00입니다 (00-20 기본적으로)을 AppContainer 및 SQL의 이름인 MSSQLSERVER 서버 인스턴스입니다.

> [!Note]
> 네트워크 호출이 필요한 경우에 Windows 방화벽의 아웃 바운드 규칙을 비활성화할 수 있습니다.

## <a name="restrict-network-access"></a>네트워크 액세스 제한

기본 설치에서는 외부 런타임 프로세스의 모든 아웃 바운드 네트워크 액세스를 차단 하도록 Windows 방화벽 규칙을 사용 됩니다. 패키지를 다운로드 하거나 악의적일 수 있는 기타 네트워크 호출 하지 못하도록 외부 런타임 프로세스를 방지 하기 위해 방화벽 규칙을 만들어야 합니다.

다른 방화벽 프로그램을 사용 하는 경우에 사용자 계정 풀이 나타내는 그룹 또는 로컬 사용자 계정에 대 한 규칙을 설정 하 여 외부 런타임에 대 한 아웃 바운드 네트워크 연결을 차단 하도록 규칙을 만들 수 있습니다.

Windows 방화벽 (또는 원하는 다른 방화벽)는 R 또는 Python 런타임에서 무제한 네트워크 액세스를 방지 하기 위해 사용 하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

[인바운드 연결에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)