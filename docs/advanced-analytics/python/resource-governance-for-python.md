---
title: "Python 용 리소스 관리 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 88f096b636dba544948410f00566c8aa3eaa0a91
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="resource-governance-for-python"></a>Python 용 리소스 관리

Python을 통해 설정 되었기 때문에 SQL Server 2016에서는 R 언어에 대 한 구현 된 동일한 확장성 아키텍처 도구 사용할 수 있습니다 기존 리소스 관리자, Dmv, 확장된 이벤트와 같은 SQL Server에서 Python의 실행을 모니터링 하려면 SQL Server의 스크립트입니다.

리소스 관리 특히는 중요 고급 하드웨어 세금 수 많은 양의 프로덕션 환경에서 데이터를 분석 합니다.  이를 수 있습니다 수 관리 되지 않거나 감사 하는 컴퓨터에 이동할 데이터베이스 외부의 데이터를 방지 하려면 데이터베이스 관리자는 고급 분석 작업에 대 한 충분 한 리소스에 할당 하는 중요 합니다.

이 섹션에서는 Python 런타임에서 사용 되는 리소스를 관리 하는 방법에 대 한 정보를 제공 및의 Python 리소스 사용 모니터링 스크립트에서 실행 하는 작업과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스.

> [!NOTE]
> Python 지원은 SQL Server 2017의 새로운 기능 하며 시험판에서 있습니다. 자세한 내용은 곧 찾습니다.
> 일반적으로 Python을 실행 하는 하나를 포함 하 여, SQL Server 2016에서 R 스크립트의 리소스 관리에 대해 제공 된 동일한 프레임 워크를 사용 하 여 모든 외부 스크립트를 모니터링할 수 있습니다.

## <a name="what-is-resource-governance"></a>리소스 관리란?

리소스 관리는 보통 지원 및 균형 유지를 위한 여러 서비스 및 여러 종속 응용 프로그램이 있는 데이터베이스 서버 환경에서 일반적으로 발생하는 문제를 식별하고 방지하도록 디자인되어 있습니다. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]의 경우 리소스 관리에는 다음 태스크가 포함됩니다.  

+ **과도 한 서버 리소스를 사용 하는 스크립트를 식별**합니다. 관리자는 너무 많은 리소스를 사용하고 있는 작업을 종료하거나 제한할 수 있어야 합니다.

+ **예측할 수 없는 작업 부하가 완화**합니다. 서버에서 동시에 실행 중인 여러 Python 작업이 리소스 풀을 사용 하 여 작업을 서로 격리 하지 않는 경우 결과 리소스 경합을 예측할 수 없는 하거나 작업의 완료를 위협 수 없습니다.

+ **작업 우선 순위 지정 순서**합니다. 관리자나 설계자는 우선 수행해야 하는 작업을 지정하거나 리소스 경합이 있는 경우 특정 작업이 완료되도록 보장할 수 있어야 합니다.

사용할 수 있습니다 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md) 외부 런타임에서 사용 하는 리소스를 관리 합니다. 이 터미널 하지만 SQL Server 컴퓨터를 사용 하 여 계산 컨텍스트로 써 실행 된 원격에서 시작 된 Python 스크립트를 포함 합니다.

> [!NOTE] 
> 리소스 관리자는 Enterprise Edition에서 사용할 수 있습니다.

## <a name="how-to-use-resource-governor-to-manage-python-execution"></a>리소스 관리자를 사용 하 여 Python 실행을 관리 하는 방법

모든 외부 스크립트 작업을 만들어 할당 된 리소스를 관리 하는 일반적으로 *외부 리소스 풀* 및 풀에 작업을 할당 합니다. 외부 리소스 풀에는 R 런타임 및 데이터베이스 엔진에 외부 다른 프로세스를 관리할 수 있도록 SQL Server 2016에 도입 된 리소스 풀의 새 형식입니다. SQL Server 2017로 시작 하는 Python 작업을 모니터링 하려면 사용할 수 있습니다.

세 가지 방법으로 기본 리소스 풀의 수 있습니다:

+ *내부 풀*은 SQL Server 자체에서 사용되는 리소스를 나타내고 변경하거나 제한할 수 없습니다.
+ *기본 풀*은 서버에 대한 리소스 사용을 전체적으로 수정하는 데 사용할 수 있는 미리 정의된 사용자 풀입니다. 이 풀에 속한 사용자 그룹을 정의하여 리소스에 대한 액세스를 관리할 수도 있습니다.
+ *기본 외부 풀*은 외부 리소스용으로 미리 정의된 사용자 풀입니다. 새 외부 리소스 풀을 만들고 이 풀에 속하는 사용자 그룹을 정의할 수도 있습니다.

또한 *사용자 정의 리소스 풀*을 만들어 데이터베이스 엔진 또는 기타 응용 프로그램에 리소스를 할당하고 *사용자 정의 외부 리소스 풀*을 만들어 R 및 기타 외부 프로세스를 관리할 수 있습니다.

용어 및 일반적인 개념에 대한 자세한 내용은 [리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)을 참조하세요.

## <a name="resource-management-using-resource-governor"></a>리소스 관리자를 사용한 리소스 관리

리소스 관리자를 처음 사용하는 경우 인스턴스 기본 리소스를 수정하고 새 외부 리소스 풀을 만드는 방법에 대한 간단한 연습을 확인하려면 [방법: R에 대한 리소스 풀 만들기](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md) 항목을 참조하세요.

사용할 수는 *외부 리소스 풀* 다음 지원 되는 실행 파일에서 사용 하는 리소스를 관리 하는 메커니즘.

+ SQL Server에서 호출 또는 SQL Server 원격 계산 컨텍스트를 원격으로 호출할 때 Python35.exe
+ BxlServer.exe 및 위성 프로세스
+ PythonLauncher.dll 등의 실행 패드에 의해 시작 아이콘

> [!NOTE]
> 리소스 관리자를 사용 하 여 실행 패드 서비스에 대 한 직접 관리 지원 되지 않습니다. 이는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]는 디자인상 Microsoft에서 제공하는 시작 관리자만 호스트할 수 있는 신뢰할 수 있는 서비스이기 때문입니다. 과도한 리소스 사용을 피하기 위해 신뢰할 수 있는 시작 관리자도 구성됩니다.

리소스 관리자를 사용하여 위성 프로세스를 관리하고 개별 데이터베이스 구성 및 작업의 요구 사항에 맞게 조정하는 것이 좋습니다.  예를 들어 실행하는 동안 요청 시 개별 위성 프로세스를 만들거나 제거할 수 있습니다.

## <a name="disable-or-enable-external-script-execution"></a>또는 외부 스크립트 실행을 사용 안 함

외부 스크립트 지원은의 경우 선택 사항 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설정 하 고 설치를 완전 하 고 외부 스크립트를 실행 한 후에은 보안상의 이유로 기본적으로 OFF로 설정 됩니다. 따라서 하나의 기계 학습 언어 및 관련된 서비스의 설치를 완료 한 후의 인스턴스를 명시적으로 다시 구성 하며 다음 데이터베이스 엔진 서비스를 다시 시작 합니다.

런어웨이 스크립트 발생할 경우 모든 스크립트 실행을 비활성화할 수 있습니다. 이 프로세스를 반대로 하 고 속성을 설정 하기만 `external scripts enabled` FALSE 또는 0 인스턴스에 있습니다. 모든 외부 스크립트 실행 바로 해제 됩니다. 보안 문제 또는 관리자가 즉시 리소스 문제를 완화 해야 하는 상황에 대해이 옵션을 예약 해야 합니다.

## <a name="see-also"></a>관련 항목:

[리소스 관리자 리소스 풀](../../relational-databases/resource-governor/resource-governor-resource-pool.md)

