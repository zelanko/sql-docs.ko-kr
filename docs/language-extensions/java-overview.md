---
title: Java 언어 확장이란?
description: SQL Server 2019에서 지원되는 언어 확장은 Java, Python, R입니다. 언어 확장은 외부 코드를 실행하는 데 사용되는 SQL Server의 기능입니다.  확장성 프레임워크를 사용하여 외부 코드에 관계형 데이터를 사용할 수 있습니다.
author: cawrites
ms.author: chadam
ms.date: 10/06/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f6b7f2c21aa79ee5c0c9657cf817d9801b5d2891
ms.sourcegitcommit: 2b6760408de3b99193edeccce4b92a2f9ed5bcc6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92175898"
---
# <a name="what-is-java-language-extension"></a>Java 언어 확장이란?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

언어 확장은 외부 코드를 실행하는 데 사용되는 SQL Server의 기능입니다. [확장성 프레임워크](concepts/extensibility-framework.md)를 사용하여 외부 코드에 관계형 데이터를 사용할 수 있습니다.

SQL Server 2019에서는 Java가 지원됩니다. 기본 Java 런타임은 Zulu Open JRE입니다. 다른 Java JRE 또는 SDK를 사용할 수도 있습니다.

> [!NOTE]
> SQL Server에서 Python 또는 R을 실행하려면 [SQL 기계 학습](../machine-learning/index.yml) 설명서를 참조하세요. SQL Server 2019 이상에서는 언어 확장과 함께 사용자 지정 Python 및 R 런타임을 사용할 수 있습니다. 자세한 내용은 [Python 사용자 지정 런타임](../machine-learning/install/custom-runtime-python.md) 및 [R 사용자 지정 런타임](../machine-learning/install/custom-runtime-r.md)을 참조하세요.

## <a name="what-you-can-do-with-language-extensions"></a>언어 확장으로 수행 가능한 작업

언어 확장은 외부 코드를 실행하는 데 확장성 프레임워크를 사용합니다. 코드 실행이 코어 엔진 프로세스에서 격리되지만 SQL Server 쿼리 실행에 완전히 통합됩니다. 데이터 원본에서 코드를 실행할 수 있으므로 네트워크를 통해 데이터를 끌어오지 않아도 됩니다.

외부 언어는 [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql)를 사용하여 정의됩니다. 시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)가 코드를 실행하기 위한 인터페이스로 사용됩니다.

언어 확장은 다양한 이점을 제공합니다.

+ 데이터 보안. 데이터 원본과 더 가까운 위치에서 외부 언어를 실행할 수 있으므로 불필요하게 또는 보안되지 않은 방식으로 데이터를 이동하지 않아도 됩니다.
+ 속도. 데이터베이스는 집합 기반 작업에 최적화됩니다. 메모리 내 테이블과 같은 최근의 데이터베이스 혁신은 요약 및 집계를 매우 신속하게 만들어 데이터 과학을 완벽하게 보완해 줍니다.
+ 손쉬운 배포 및 통합. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]는 여러 다른 데이터 관리 작업 및 애플리케이션에 대한 중앙 운영 지점입니다. 데이터베이스의 데이터를 사용하여 Java에서 사용하는 데이터가 일관되며 최신 상태로 유지되도록 할 수 있습니다.

## <a name="how-to-get-started"></a>시작하는 방법

### <a name="step-1-install-the-software"></a>1단계: 소프트웨어 설치

+ [Windows에 SQL Server 언어 확장 설치](install/windows-java.md)
+ [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)

### <a name="step-2-configure-a-development-tool"></a>2단계: 개발 도구 구성

개발자는 일반적으로 자체 노트북 또는 개발 워크스테이션에서 코드를 작성합니다. SQL Server에서 언어 확장을 사용하는 경우 이 프로세스를 변경할 필요가 없습니다. 설치가 완료되면 SQL Server에서 Java 코드를 실행할 수 있습니다.

+ Java 코드 개발에는 **선호하는 IDE를 사용** 합니다.

+ SQL Server에서 Java 코드를 실행하려면 **[Microsoft 확장성 SDK for Java](how-to/extensibility-sdk-java-sql-server.md) 를 설치** 합니다.

+ SQL Server에서 외부 코드를 실행하는 데는 **[Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) 또는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용** 합니다.

+ SQL Server에서 Java 코드를 실행하려면 **시스템 저장 프로시저 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)를 사용** 합니다.

### <a name="step-3-write-your-first-code"></a>3단계: 첫 번째 코드 작성

T-SQL 스크립트 내에서 Java 코드를 실행합니다.

+ [자습서: Java를 사용하는 정규식](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>제한 사항

+ 입력 및 출력 버퍼의 값 개수가 Java의 배열에서 할당될 수 있는 최대 요소 수인 `MAX_INT (2^31-1)`를 초과할 수 없습니다.

## <a name="next-steps"></a>다음 단계

+ [SQL Server용 Python 사용자 지정 런타임](../machine-learning/install/custom-runtime-python.md) 설치
+ [SQL Server용 R 사용자 지정 런타임](../machine-learning/install/custom-runtime-r.md) 설치
+ [Windows에 SQL Server 언어 확장 설치](../language-extensions/install/windows-java.md) 또는 [Linux에 SQL Server 언어 확장 설치](../linux/sql-server-linux-setup-language-extensions-java.md)
+ [Java 용 Microsoft 확장성 SDK](how-to/extensibility-sdk-java-sql-server.md) 설치
