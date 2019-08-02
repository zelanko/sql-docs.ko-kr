---
title: R 스크립팅 오류 및 문제 해결
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 10ec78bf8627bfef3232dfc72d7ef7f638604b15
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715751"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server에서 R 스크립팅 오류
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server에서 R 코드를 실행할 때의 여러 스크립팅 오류에 대해 설명 합니다. 목록은 포괄적이 지 않습니다. 많은 패키지가 있으며, 동일한 패키지의 버전 마다 오류가 다를 수 있습니다. R Services (데이터베이스 내), Microsoft R Client 및 Microsoft R Server에서 사용 되는 기계 학습 구성 요소를 지 원하는 [Machine Learning Server 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR)에 스크립트 오류를 게시 하는 것이 좋습니다.

## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-sql 또는 저장 프로시저에서 올바른 스크립트가 실패 합니다.

저장 프로시저에서 R 코드를 래핑 하기 전에 외부 IDE 또는 RTerm 또는 Rterm와 같은 R 도구 중 하나에서 R 코드를 실행 하는 것이 좋습니다. 이러한 메서드를 사용 하 여 R에서 반환 하는 자세한 오류 메시지를 사용 하 여 코드를 테스트 하 고 디버그할 수 있습니다.

그러나 외부 IDE 또는 유틸리티에서 완벽 하 게 작동 하는 코드는 저장 프로시저 또는 SQL Server 계산 컨텍스트에서 실행 되지 않을 수 있습니다. 이러한 상황이 발생 하는 경우 패키지가 SQL Server에서 작동 하지 않는다고 가정할 수 있도록 하기 위해 다양 한 문제를 찾아야 합니다.

1. 실행 패드가 실행 중인지 여부를 확인 합니다.

2. 메시지를 검토 하 여 입력 데이터 또는 출력 데이터에 호환 되지 않거나 지원 되지 않는 데이터 형식의 열이 포함 되어 있는지 확인 합니다. 예를 들어 SQL database에 대 한 쿼리는 종종 Guid 또는 RowGUIDs를 반환 하며, 둘 다 지원 되지 않습니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)을 참조 하세요.

3. 개별 R 함수에 대 한 도움말 페이지를 검토 하 여 모든 매개 변수가 SQL Server 계산 컨텍스트에 지원 되는지 여부를 확인 합니다. ScaleR 도움말을 보려면 인라인 R 도움말 명령을 사용 하거나 [패키지 참조](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)를 참조 하세요.

R 런타임이 작동 하지만 스크립트에서 오류를 반환 하는 경우 Visual Studio용 R 도구와 같은 전용 R 개발 환경에서 스크립트 디버깅을 시도 하는 것이 좋습니다.

또한 R과 데이터베이스 엔진 간에 데이터를 이동할 때 발생할 수 있는 데이터 형식의 문제를 해결 하기 위해 스크립트를 검토 하 고 약간 다시 작성 하는 것이 좋습니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)을 참조 하세요.

또한 sqlrutils 패키지를 사용 하 여 R 스크립트를 저장 프로시저로 더 쉽게 사용 되는 형식으로 묶을 수 있습니다. 참조 항목:
* [sqlrutils 패키지](r/ref-r-sqlrutils.md)
* [Sqlrutils를 사용 하 여 저장 프로시저 만들기](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>스크립트가 일관 되지 않은 결과를 반환 합니다.

R 스크립트는 다음과 같은 여러 가지 이유로 SQL Server 컨텍스트에서 다른 값을 반환할 수 있습니다.

- SQL Server와 R 간에 데이터가 전달 되는 경우 일부 데이터 형식에 대해 암시적 형식 변환이 자동으로 수행 됩니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)을 참조 하세요.

- 비트가 요소 인지 여부를 확인 합니다. 예를 들어 32 비트 및 64 비트 부동 소수점 라이브러리에 대 한 수치 연산 결과에는 종종 차이가 있습니다.

- Nan가 작업에서 생성 되었는지 여부를 확인 합니다. 이로 인해 결과가 무효화 될 수 있습니다.

- 숫자의 역 수가 0에 도달 하면 작은 차이를 증폭 시킬 수 있습니다.

- 누적 된 반올림 오류는 0이 아닌 0 보다 작은 값으로 인해 발생할 수 있습니다.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC를 통한 원격 실행을 위한 묵시적 인증

RevoScaleR 함수를 사용 하 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 여 R 명령을 실행 하기 위해 컴퓨터에 연결 하는 경우 서버에 데이터를 쓰는 ODBC 호출을 사용 하면 오류가 발생할 수 있습니다. 이 오류는 Windows 인증을 사용 하는 경우에만 발생 합니다.

그 이유는 R Services에 대해 만들어진 작업자 계정에 서버에 연결할 수 있는 권한이 없기 때문입니다. 따라서 ODBC 호출은 사용자를 대신 하 여 실행할 수 없습니다. Sql 로그인을 사용 하면 R 클라이언트에서 SQL Server 인스턴스로 명시적으로 전달 된 다음 ODBC에 자격 증명이 전달 되기 때문에 SQL 로그인에 문제가 발생 하지 않습니다. 그러나 SQL 로그인을 사용 하는 것은 Windows 인증을 사용 하는 것 보다 더 안전 하지 않습니다.

원격으로 시작 된 스크립트에서 Windows 자격 증명을 안전 하 게 전달할 수 있도록 하려면 SQL Server 자격 증명을 에뮬레이션 해야 합니다. 이 프로세스는 _암시적 인증_이라고 합니다. 이 작업을 수행 하려면 SQL Server 컴퓨터에서 R 또는 Python 스크립트를 실행 하는 작업자 계정에 올바른 권한이 있어야 합니다.

1. R [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 코드를 실행 하려는 인스턴스에서 관리자 권한으로를 엽니다.

2. 다음 스크립트를 실행합니다. 기본값, 컴퓨터 및 인스턴스 이름을 변경한 경우 사용자 그룹 이름을 편집 해야 합니다.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 계산 컨텍스트에서 R을 실행 하는 동안 작업 영역을 지우지 마십시오.

R 콘솔에서 작업 하는 경우 작업 영역을 제거 하는 것이 일반적 이지만 의도 하지 않은 결과를 SQL 계산 컨텍스트에서 사용할 수 있습니다.

`revoScriptConnection`는 SQL Server에서 호출 되는 R 세션에 대 한 정보를 포함 하는 R 작업 영역에 있는 개체입니다. 그러나 r 코드에 작업 영역을 지우는 명령 (예: `rm(list=ls())`)이 포함 되어 있는 경우에는 r 작업 영역의 세션 및 기타 개체에 대 한 모든 정보도 지워집니다.

이 문제를 해결 하려면 SQL Server에서 R을 실행 하는 동안 변수 및 기타 개체를 무분별 지우지 마십시오. **Remove** 함수를 사용 하 여 특정 변수를 삭제할 수 있습니다.

```R
remove('name1', 'name2', ...)
```

삭제할 변수가 여러 개 있는 경우에는 임시 변수의 이름을 목록에 저장 한 다음 목록에서 주기적 가비지 수집을 수행 하는 것이 좋습니다.



## <a name="next-steps"></a>다음 단계

[Machine Learning Services 문제 해결 및 알려진 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결을 위한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
