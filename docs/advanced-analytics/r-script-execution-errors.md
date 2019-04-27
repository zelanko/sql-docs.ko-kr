---
title: R 스크립팅 오류 및 문제 해결-SQL Server Machine Learning 서비스
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 2df4fa2fd9ef52fe5edbca9440f73f351553f1ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642345"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server에서 R 스크립트 오류
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server에서 R 코드를 실행 하는 경우 여러 scriptin gerrors를 설명 합니다. 목록 포괄적인 아닙니다. 많은 패키지 되며 오류는 동일한 패키지의 버전 간에 달라질 수 있습니다. 스크립트 오류를 게시 하는 것이 좋습니다 합니다 [Machine Learning Server 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=MicrosoftR), 기계 학습 R Services (In-database), Microsoft R Client 및 Microsoft R Server에 사용 되는 구성 요소를 지 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 Machine Learning 서비스


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>저장된 프로시저 또는 T-SQL에서 유효한 스크립트 실패

저장된 프로시저에서 R 코드를 래핑하기 전에 RGui 또는 RTerm 같은 R 도구 중 하나에서 또는 외부 IDE에서 R 코드를 실행 하는 것이 좋습니다. 이러한 메서드를 사용 하 여 테스트 및 R에서 반환 되는 자세한 오류 메시지를 사용 하 여 코드를 디버깅할 수 있습니다.

그러나 경우에 따라 저장된 프로시저에서 실행 하거나 SQL server에서 계산 컨텍스트를 외부 IDE 또는 유틸리티에서 완벽 하 게 작동 하는 코드 실패할 수 있습니다. 이런 경우 다양 한 문제를 검색할 전에 패키지를 SQL Server에서는 작동 하지 않습니다는 가정할 수 있습니다.

1. 실행 패드 실행 중인지 여부를 확인 합니다.

2. 데이터 입력된 또는 출력 데이터 호환 되지 않거나 지원 되지 않는 데이터 형식의 열을 포함 하는지 여부를 확인 하려면 메시지를 검토 합니다. 예를 들어, SQL database에 대 한 쿼리 Guid 또는 RowGUIDs, 둘 다 지원 되지 않는 자주 반환 합니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

3. 모든 매개 변수는 SQL Server 계산 컨텍스트에서 지원 하는지 여부를 확인 하려면 개별 R 함수에 대 한 도움말 페이지를 검토 합니다. ScaleR 도움말에 대 한 인라인 R 도움말 명령을 사용 하 여 또는 참조 [패키지 참조](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)합니다.

R 런타임을 작동 하는 스크립트 오류를 반환 합니다. 그러나 하는 경우에 Visual Studio 용 R 도구와 같은 전용된 R 개발 환경에서 스크립트 디버깅을 시도 하는 것이 좋습니다.

검토 하 고 약간 데이터베이스 엔진과 R 간에 데이터를 이동할 때 발생할 수 있는 데이터 형식 사용 하 여 문제를 해결 하려면 스크립트를 다시 작성 하는 것이 좋습니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

또한 저장된 프로시저를 보다 쉽게 사용 되는 형식에서 R 스크립트 번들로 묶는 sqlrutils 패키지를 사용할 수 있습니다. 참조 항목:
* [sqlrutils package](r/ref-r-sqlrutils.md)
* [Sqlrutils를 사용 하 여 저장된 프로시저 만들기](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>스크립트 일관 되지 않은 결과 반환합니다.

R 스크립트 여러 가지 이유로 SQL Server 컨텍스트에서 다른 값을 반환할 수 있습니다.

- SQL Server 및 R 간에 데이터 전달 될 때 일부 데이터 형식에서 암시적 형식 변환은 자동으로 수행 됩니다. 자세한 내용은 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

- 비트 요소 인지 확인 합니다. 예를 들어, 종종에 차이가 32 비트 및 64 비트 부동 지점 라이브러리에 대 한 수치 연산의 결과입니다.

- 모든 작업에 nan이 생성 된 여부를 결정 합니다. 결과가 무효화 될 수 있습니다.

- 0에 가까운 숫자의 역을 가져올 때에 작은 차이점을 증폭 될 수 있습니다.

- 누적 된 반올림 오류 등의 값을 0이 아닌 0 보다 작은 경우 발생할 수 있습니다.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC 통한 원격 실행을 위해 암시적된 인증

연결 하는 경우는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R을 실행 하는 컴퓨터를 사용 하 여 명령 합니다 **RevoScaleR** 함수 오류가 발생할 수 있습니다는 서버에 데이터를 기록 하는 ODBC 호출을 사용 하는 경우. 이 오류는 Windows 인증을 사용 하는 경우에 발생 합니다.

원인은 작업자 계정이 R Services에 대해 생성 된 서버에 연결할 수 있는 권한이 없는 것입니다. 따라서 사용자 대신 ODBC 호출을 실행할 수 없습니다. SQL 로그인을 사용 하 여 자격 증명을 명시적으로 전달 된 R 클라이언트에서 SQL Server 인스턴스 및 ODBC 때문에 SQL 로그인을 사용 하 여 문제가 발생 하지 않습니다. 그러나 SQL 로그인을 사용 하 여 이기도 Windows 인증을 사용 하 여 보다 덜 안전 합니다.

시작 된 원격으로 SQL Server는 스크립트에서 안전 하 게 전달 될 Windows 자격 증명을 사용 하도록 설정 하려면 자격 증명을 에뮬레이트할 해야 합니다. 이 프로세스 라고 _묵시적된 인증_합니다. 이 작업을 하려면 SQL Server 컴퓨터에서 R 또는 Python 스크립트를 실행 하는 작업자 계정에 올바른 사용 권한이 있어야 합니다.

1. 열기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] R 코드를 실행 하려는 인스턴스에서 관리자 권한으로 합니다.

2. 다음 스크립트를 실행합니다. 기본값을 변경한 경우 사용자 그룹 이름 및 컴퓨터 및 인스턴스 이름을 편집 해야 합니다.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 계산 컨텍스트에서 R을 실행 하는 동안 작업 영역을 지우지 마세요

수 있는 경우에 작업 영역을 지우는 공통 R 콘솔에서 작업할 때 의도 하지 않은 결과 sql에서 계산 컨텍스트.

`revoScriptConnection` SQL Server에서 호출 되는 R 세션에 대 한 정보를 포함 하는 R 작업 영역의 개체가입니다. 그러나 R 코드를 작업 영역을 선택 취소 하기 위한 명령을 포함 하는 경우 (같은 `rm(list=ls())`), 세션 및 R 작업 영역에서 다른 개체에 대 한 모든 정보도 지워집니다.

해결 방법으로 SQL Server에서 R을 실행 하는 동안 변수 및 기타 개체를 무차별 지우지 마세요. 사용 하 여 특정 변수를 삭제할 수 있습니다 합니다 **제거** 함수:

```R
remove('name1', 'name2', ...)
```

삭제할 변수가 여러 경우에 임시 변수 이름이 목록에 저장 한 다음 목록에 주기적 가비지 수집을 수행 하는 것이 좋습니다.



## <a name="next-steps"></a>다음 단계

[Machine Learning Services 문제 해결 및 알려진된 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
