---
title: 일반적인 R 스크립팅 오류
description: 이 문서에서는 SQL Server에서 R 코드를 실행할 때 발생할 수 있는 여러 일반적인 스크립팅 오류에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2982a0d449d031ba6f211f29a919c588a507a4ba
ms.sourcegitcommit: 04fb4c2d7ccddd30745b334b319d9d2dd34325d6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89569931"
---
# <a name="common-r-scripting-errors-in-sql-server"></a>SQL Server에서 일반적인 R 스크립팅 오류
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 SQL Server에서 R 코드를 실행할 때의 여러 일반적인 스크립팅 오류에 대해 설명합니다. 이 목록에는 일부만 나와 있습니다. 다양한 패키지가 있으며 동일한 패키지도 버전마다 오류가 다를 수 있습니다.

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-SQL 또는 저장 프로시저에서 올바른 스크립트가 실패

저장 프로시저에서 R 코드를 래핑하기 전에 외부 IDE 또는 RTerm이나 RGui와 같은 R 도구 중 하나에서 R 코드를 실행하는 것이 좋습니다. 이러한 메서드를 사용하면 R에서 반환하는 자세한 오류 메시지를 통해 코드를 테스트하고 디버그할 수 있습니다.

그러나 외부 IDE 또는 유틸리티에서 완벽하게 작동하는 코드는 저장 프로시저 또는 SQL Server 컴퓨팅 컨텍스트에서 실행되지 않을 수 있습니다. 이런 일이 발생하면 SQL Server에서 패키지가 작동하지 않는다고 가정하기 전에 살펴봐야 할 다양한 문제가 있습니다.

1. 실행 패드의 실행 여부를 확인합니다.

2. 메시지를 검토하여 입력 데이터 또는 출력 데이터에 호환되지 않거나 지원되지 않는 데이터 형식의 열이 포함되어 있는지 확인합니다. 예를 들어 SQL 데이터베이스에 대한 쿼리는 종종 GUID 또는 RowGUID를 반환하며, 둘 다 지원되지 않습니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

3. 개별 R 함수에 대한 도움말 페이지를 검토하여 모든 매개 변수가 SQL Server 컴퓨팅 컨텍스트에 지원되는지 여부를 확인합니다. ScaleR 도움말을 보려면 인라인 R 도움말 명령을 사용하거나 [패키지 참조](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)를 확인하세요.

R 런타임이 작동하지만 스크립트에서 오류를 반환하는 경우 Visual Studio용 R 도구와 같은 전용 R 개발 환경에서 스크립트 디버깅을 시도하는 것이 좋습니다.

또한 R과 데이터베이스 엔진 간에 데이터를 이동할 때 발생할 수 있는 데이터 형식의 문제를 해결하기 위해 스크립트를 검토하고 약간 다시 작성하는 것이 좋습니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

또한 sqlrutils 패키지를 사용하면 저장 프로시저로 더 쉽게 사용되는 형식으로 R 스크립트를 번들로 포함할 수 있습니다. 자세한 내용은 다음을 참조하세요.
* [sqlrutils 패키지](../r/ref-r-sqlrutils.md)
* [sqlrutils를 사용하여 저장 프로시저 만들기](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>스크립트가 일관되지 않은 결과를 반환

R 스크립트는 다음과 같은 여러 가지 이유로 SQL Server 컨텍스트에서 다른 값을 반환할 수 있습니다.

- SQL Server와 R 간에 데이터가 전달될 때 일부 데이터 형식에 대해 암시적 형식 변환이 자동으로 수행됩니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](../r/r-libraries-and-data-types.md)을 참조하세요.

- 비트 수가 요인인지 여부를 확인합니다. 예를 들어 32비트 및 64비트 부동 소수점 라이브러리에 대한 수학 연산 결과에는 종종 차이가 있습니다.

- NaN이 작업에서 생성되었는지 여부를 확인합니다. 이로 인해 결과가 무효화될 수 있습니다.

- 작은 차이는 0에 가까운 숫자의 역수를 취할 때 증폭될 수 있습니다.

- 누적된 반올림 오류는 0이 아닌 0보다 작은 값으로 인해 발생할 수 있습니다.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC를 통한 원격 실행을 위한 암시적 인증

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 연결하여 **RevoScaleR** 함수로 R 명령을 실행하는 경우 서버에 데이터를 기록하는 ODBC 호출을 사용할 때 오류가 발생할 수 있습니다. 이 오류는 Windows 인증을 사용하는 경우에만 발생합니다.

그 이유는 R Services에 대해 만들어진 작업자 계정에 서버에 연결할 수 있는 권한이 없기 때문입니다. 따라서 ODBC 호출은 사용자를 대신하여 실행할 수 없습니다. SQL 로그인을 사용하면 자격 증명이 R 클라이언트에서 SQL Server 인스턴스로 명시적으로 전달된 다음, ODBC에 전달되기 때문에 SQL 로그인에 문제가 발생하지 않습니다. 그러나 SQL 로그인 사용은 Windows 인증을 사용하는 것보다 안전성이 더 떨어집니다.

원격으로 시작된 스크립트에서 Windows 자격 증명을 안전하게 전달할 수 있도록 하려면 SQL Server에서 자격 증명을 에뮬레이션해야 합니다. 이 프로세스를 _암시적 인증_이라고 합니다. 이 작업을 수행하려면 SQL Server 컴퓨터에서 R 또는 Python 스크립트를 실행하는 작업자 계정에 올바른 권한이 있어야 합니다.

1. R 코드를 실행할 인스턴스에서 관리자 권한으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다.

2. 다음 스크립트를 실행합니다. 기본값, 컴퓨터 및 인스턴스 이름을 변경한 경우 사용자 그룹 이름을 편집해야 합니다.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 컴퓨팅 컨텍스트에서 R을 실행하는 동안 작업 영역을 지우지 마십시오.

R 콘솔에서 작업할 때 작업 영역을 지우는 것은 일반적이지만, SQL 컴퓨팅 컨텍스트에서 의도하지 않은 결과가 발생할 수 있습니다.

`revoScriptConnection`은 SQL Server에서 호출된 R 세션에 대한 정보를 포함하는 R 작업 영역의 개체입니다. 그러나 R 코드에 작업 영역을 지우는 명령(예: `rm(list=ls())`)이 포함되어 있으면 세션 및 R 작업 영역의 다른 개체에 대한 모든 정보도 지워집니다.

해결 방법은 SQL Server에서 R을 실행하는 동안에는 변수 및 기타 개체를 무차별적으로 지우지 않는 것입니다. **remove** 함수를 사용하면 특정 변수를 삭제할 수 있습니다.

```R
remove('name1', 'name2', ...)
```

삭제할 변수가 여러 개인 경우 임시 변수 이름을 목록에 저장한 다음, 목록에서 주기적 가비지 수집을 수행합니다.



## <a name="next-steps"></a>다음 단계

[Machine Learning Services 문제 해결 및 알려진 문제](machine-learning-troubleshooting-overview.md)

[기계 학습 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[SQL Server Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)

[데이터베이스 엔진 연결 문제 해결](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
