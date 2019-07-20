---
title: 방화벽 구성
description: SQL Server Machine Learning Services에서 아웃 바운드 연결에 대 한 방화벽을 구성 하는 방법입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 58a10c36eff06cd4e36f3e326407564b2657fec1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345600"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에 대 한 방화벽 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에는 machine learning 서비스를 사용할 때 관리자나 설계자가 염두에 두어야 하는 방화벽 구성 고려 사항이 나열 되어 있습니다.

## <a name="default-firewall-rules"></a>기본 방화벽 규칙

기본적으로 SQL Server 설치 프로그램은 방화벽 규칙을 만들어 아웃 바운드 연결을 사용 하지 않도록 설정 합니다.

SQL Server 2016 및 2017에서 이러한 규칙은 로컬 사용자 계정을 기반으로 합니다 .이 규칙은 설치 프로그램이 해당 구성원에 대 한 네트워크 액세스를 거부 한 **SQLRUserGroup** 에 대 한 아웃 바운드 규칙 하나를 만들었습니다 (각 작업자 계정은 규칙에 따라 로컬 주체로 나열 됨). SQLRUserGroup에 대 한 자세한 내용은 [SQL Server Machine Learning Services 확장성 프레임 워크의 보안 개요](../../advanced-analytics/concepts/security.md#sqlrusergroup)를 참조 하세요.

SQL Server 2019에서 AppContainers으로 이동 하는 과정의 일부로, SQL Server 설치 프로그램에서 생성 하는 20 개 AppContainers 각각에 해당 하는 새 방화벽 규칙이 AppContainer Sid를 기반으로 합니다. 방화벽 규칙 이름에 대 한 명명 규칙은 **SQL Server 인스턴스 MSSQLSERVER의 appcontainer-00에 대 한 네트워크 액세스를 차단**합니다. 여기서 00은 appcontainer의 수 (00-20)입니다. MSSQLSERVER는 SQL Server 인스턴스의 이름입니다.

> [!Note]
> 네트워크 호출이 필요한 경우 Windows 방화벽에서 아웃 바운드 규칙을 사용 하지 않도록 설정할 수 있습니다.

## <a name="restrict-network-access"></a>네트워크 액세스 제한

기본 설치에서 Windows 방화벽 규칙은 외부 런타임 프로세스의 모든 아웃 바운드 네트워크 액세스를 차단 하는 데 사용 됩니다. 외부 런타임 프로세스가 패키지를 다운로드 하거나 악의적인 가능성이 있는 다른 네트워크 호출을 수행 하지 못하도록 방화벽 규칙을 만들어야 합니다.

다른 방화벽 프로그램을 사용 하는 경우 로컬 사용자 계정 또는 사용자 계정 풀이 나타내는 그룹에 대해 규칙을 설정 하 여 외부 런타임에 대 한 아웃 바운드 네트워크 연결을 차단 하는 규칙을 만들 수도 있습니다.

R 또는 Python 런타임에서 무제한 네트워크 액세스를 방지 하려면 Windows 방화벽 (또는 원하는 다른 방화벽)을 설정 하는 것이 좋습니다.

## <a name="next-steps"></a>다음 단계

[바인딩된 연결에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)