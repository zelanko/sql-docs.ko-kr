---
title: 방화벽 구성
description: SQL Server Machine Learning Services에서 아웃바운드 연결에 대한 방화벽을 구성하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/17/2018
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 44fa8b361f74fb670dd5671bb9fbeaa9e635faad
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470704"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대한 방화벽 구성
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에는 Machine Learning Services를 사용할 때 관리자나 설계자가 염두에 두어야 하는 방화벽 구성 고려 사항이 나열되어 있습니다.

## <a name="default-firewall-rules"></a>기본 방화벽 규칙

기본적으로 SQL Server 설치 프로그램은 방화벽 규칙을 만들어 아웃바운드 연결을 사용하지 않도록 설정합니다.

SQL Server 2016 및 2017에서는 이러한 규칙이 로컬 사용자 계정을 기준으로 했습니다. 이 경우 설치 프로그램은 해당 멤버에 대한 네트워크 액세스를 거부하는 **SQLRUserGroup** 에 대한 아웃바운드 규칙을 하나 만들었습니다(각 작업자 계정은 rule_에 적용되는 로컬 주체로 나열됨). SQLRUserGroup에 대한 자세한 내용은 [SQL Server Machine Learning Services의 확장성 프레임워크에 대한 보안 개요](../../machine-learning/concepts/security.md#sqlrusergroup)를 참조 하세요.

SQL Server 2019에서는 AppContainer로 전환하는 과정에서 AppContainer SID를 기준으로 새로운 방화벽 규칙이 생성되었습니다. 각 규칙은 SQL Server 설치 프로그램에서 만든 20개의 AppContainer 각각에 해당합니다. 방화벽 규칙 이름에 대한 명명 규칙은 **SQL Server 인스턴스 MSSQLSERVER에서 AppContainer-00에 대한 네트워크 액세스 차단** 입니다. 여기서 00은 AppContainer의 번호(기본적으로 00-20)이고 MSSQLSERVER는 SQL Server 인스턴스의 이름입니다.

> [!Note]
> 네트워크 호출이 필요한 경우 Windows 방화벽에서 아웃바운드 규칙을 사용하지 않도록 설정할 수 있습니다.

## <a name="restrict-network-access"></a>네트워크 액세스 제한

기본 설치에서는 Windows 방화벽 규칙을 사용하여 외부 런타임 프로세스의 모든 아웃바운드 네트워크 액세스를 차단합니다. 외부 런타임 프로세스가 패키지를 다운로드하거나 악의적일 수 있는 기타 네트워크 호출을 수행하지 못하도록 하려면 방화벽 규칙을 만들어야 합니다.

다른 방화벽 프로그램을 사용하는 경우에는 로컬 사용자 계정 또는 사용자 계정 풀이 나타내는 그룹에 대해 규칙을 설정하여 외부 런타임에 대해 아웃바운드 네트워크 연결을 차단할 수도 있습니다.

Windows 방화벽 또는 원하는 기타 방화벽을 설정해 R 또는 Python 런타임의 제한없는 네트워크 액세스를 방지하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

[인바운드 연결에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)