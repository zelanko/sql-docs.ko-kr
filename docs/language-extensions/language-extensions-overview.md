---
title: SQL Server 언어 확장이란?
titleSuffix: ''
description: 언어 확장은 외부 코드를 실행하는 데 사용되는 SQL Server의 기능입니다. SQL Server에서는 Java, Python, R이 지원됩니다. 확장성 프레임워크를 사용하여 외부 코드에 관계형 데이터를 사용할 수 있습니다.
author: dphansen
ms.author: davidph
ms.date: 11/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e62b61e2b90f3a2f3ec837115d99a65070571c57
ms.sourcegitcommit: 06cb1751b1bc7420dbe4ad4555ab1afc5fc5bd71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361754"
---
# <a name="what-is-sql-server-language-extensions"></a>SQL Server 언어 확장이란?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

언어 확장은 외부 코드를 실행하는 데 사용되는 SQL Server의 기능입니다. [확장성 프레임워크](concepts/extensibility-framework.md)를 사용하여 외부 코드에 관계형 데이터를 사용할 수 있습니다. SQL Server 2019에서는 Java, Python, R 런타임이 지원됩니다.

> [!NOTE]
> SQL Server에서 Python 또는 R을 실행하는 방법에 대한 자세한 내용은 [Machine Learning Services](../machine-learning/sql-server-machine-learning-services.md) 설명서를 참조하세요. SQL Server 2019 이상에서는 언어 확장과 함께 사용자 지정 Python 및 R 런타임을 사용할 수 있습니다. 자세한 내용은 [Python 사용자 지정 런타임](../machine-learning/install/custom-runtime-python.md) 및 [R 사용자 지정 런타임](../machine-learning/install/custom-runtime-r.md) 설치 방법을 참조하세요.

## <a name="what-you-can-do-with-language-extensions"></a>언어 확장으로 수행 가능한 작업

언어 확장은 외부 코드를 실행하는 데 [확장성 프레임워크](concepts/extensibility-framework.md)를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다. 데이터 원본에서 코드를 실행할 수 있으므로 네트워크를 통해 데이터를 끌어오지 않아도 됩니다.

외부 언어는 [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md)를 사용하여 정의됩니다. 시스템 저장 프로시저 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)가 코드를 실행하기 위한 인터페이스로 사용됩니다.

언어 확장은 다음과 같은 여러 이점을 제공합니다.

+ 데이터 보안. 데이터 원본과 더 가까운 위치에서 외부 언어를 실행할 수 있으므로 보안되지 않은 방식으로 데이터를 이동하지 않아도 됩니다.
+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 
+ 손쉬운 배포 및 통합. [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)]는 여러 다른 데이터 관리 작업 및 애플리케이션에 대한 중앙 운영 지점입니다. 데이터베이스 데이터를 사용하여 언어 확장에서 사용되는 데이터의 일관성과 최신 상태를 보장합니다.

## <a name="next-steps"></a>다음 단계

+ [Windows에 SQL Server 언어 확장 설치](install/windows-java.md) 또는 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)
+ [SQL Server용 Python 사용자 지정 런타임](../machine-learning/install/custom-runtime-python.md) 설치
+ [SQL Server용 R 사용자 지정 런타임](../machine-learning/install/custom-runtime-r.md) 설치
+ [Java 용 Microsoft 확장성 SDK](how-to/extensibility-sdk-java-sql-server.md) 설치
