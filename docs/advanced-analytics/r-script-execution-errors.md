---
title: SQL Server 기계 학습 및 R 서비스에서 R 스크립트 오류 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0b695111849b234f6ca38fc89c538e905f187fb6
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34709108"
---
# <a name="r-scripting-errors-in-sql-server"></a>SQL Server에서 R 스크립트 오류
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 SQL Server에서 R 코드를 실행할 때 몇 가지 scriptin gerrors를 설명 합니다. 목록이 불과합니다. 많은 패키지 및 오류는 동일한 패키지의 버전 간에 달라질 수 있습니다. 스크립트 오류를 게시 하는 것이 좋습니다는 [컴퓨터 학습 서버 포럼](https://social.msdn.microsoft.com/Forums/home?category=MicrosoftR), 더욱 기계 학습 R Services (In-database), Microsoft R Client 및 Microsoft R Server에 사용 되는 구성 요소를 지원 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스


## <a name="valid-script-fails-in-t-sql-or-in-stored-procedures"></a>T-SQL에서 또는 저장된 프로시저에서 올바른 스크립트 실패

저장된 프로시저에서 R 코드를 배치 하기 전에 외부 IDE에서 또는 rterm이 또는 관리자 권한 같은 R 도구 중 하나에서 R 코드를 실행 하 것이 좋습니다. 이 메서드를 사용 하 여 테스트 하 고 오른쪽에서 반환 되는 자세한 오류 메시지를 사용 하 여 코드를 디버깅 합니다.

그러나 경우에 따라 저장된 프로시저에서 실행 하거나 계산 컨텍스트는 SQL Server에서 외부 IDE 또는 유틸리티에서 완벽 하 게 작동 하는 코드 실패할 수 있습니다. 이런 경우가 발생 하는 경우 패키지 SQL Server에서 작동 하지 않는 가정할 수 전에 찾아봐야 할 문제는 여러 가지 사항이 있습니다.

1. 실행 패드 실행 중인지 여부를 확인 합니다.

2. 입력된 데이터 또는 출력 데이터 호환 되지 않거나 지원 되지 않는 데이터 형식 열이 포함 되어 있는지 여부를 확인 하려면 메시지를 검토 합니다. 예를 들어 SQL 데이터베이스에 대 한 쿼리 Guid 또는 지원 되지 않습니다는 RowGUIDs 자주 반환 합니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

3. SQL Server 계산 컨텍스트에서 대 한 모든 매개 변수 지원 되는지 여부를 확인 하려면 개별 R 함수에 대 한 도움말 페이지를 검토 합니다. ScaleR 도움말에 대 한 인라인 R 도움말 명령을 사용 하거나 참조 [패키지 참조](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)합니다.

R 런타임 작동 하는 경우 오류를 반환 하는 스크립트는 전용된 등의 R 개발 환경 R Tools for Visual Studio에서에서 스크립트를 디버깅 하려고 하는 것이 좋습니다.

검토 하 고 약간 R과 데이터베이스 엔진 간에 데이터를 이동할 때 발생할 수 있는 데이터 형식 문제를 해결 하는 스크립트를 다시 작성 하는 것이 좋습니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

또한 R 스크립트를 보다 쉽게 저장 프로시저로 사용 되는 형식으로 번들로 묶는 sqlrutils 패키지를 사용할 수 있습니다. 참조 항목:
* [Sqlrutils 패키지를 사용 하 여 R 코드에 대 한 저장된 프로시저를 생성 합니다.](r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)
* [Sqlrutils를 사용 하 여 저장된 프로시저 만들기](r/how-to-create-a-stored-procedure-using-sqlrutils.md)

## <a name="script-returns-inconsistent-results"></a>스크립트 일관 되지 않은 결과 반환합니다.

R 스크립트 여러 가지 이유로 SQL Server 컨텍스트에서 서로 다른 값을 반환할 수 있습니다.

- 데이터는 SQL Server와 오른쪽 간에 전달 될 때 일부 데이터 형식에 암시적 형식 변환은 자동으로 수행 됩니다. 자세한 내용은 참조 [R 라이브러리 및 데이터 형식](r/r-libraries-and-data-types.md)합니다.

- 비트는 요소 인지 확인 합니다. 예를 들어 32 비트 및 64 비트 부동 지점 라이브러리에 대 한 수치 연산의 결과의 차이 종종 됩니다.

- Nan 작업에서 생성 된 여부를 결정 합니다. 결과 무효화 될 수 있습니다.

- 0에 가까운 숫자의 역을 수행할 때 방법 차이로 증폭 수 있습니다.

- 누적 된 반올림 오류 등의 작업 하는 0이 아닌 0 보다 작은 값으로 발생할 수 있습니다.

## <a name="implied-authentication-for-remote-execution-via-odbc"></a>ODBC 통해 원격 실행에 대 한 묵시적된 인증

에 연결 하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] R을 실행할 컴퓨터를 사용 하 여 명령을 **RevoScaleR** 함수를 서버에 데이터를 기록 하는 ODBC 호출을 사용 하는 경우 오류가 발생할 수 있습니다. 이 오류는 Windows 인증을 사용 하는 경우에 발생 합니다.

원인은 R Services 용으로 작성 된 작업자 계정은 서버에 연결할 수 있는 권한이 없는 것입니다. 따라서 사용자 대신 ODBC 호출을 실행할 수 없습니다. SQL 로그인이 있는 자격 증명 전달 되기 때문에 명시적으로 R 클라이언트로부터 SQL Server 인스턴스 및 ODBC SQL 로그인이 있는 문제가 발생 하지 않습니다. 그러나 SQL 로그인을 사용 하 여 이기도 Windows 인증을 사용 하 여 보다 덜 안전 합니다.

사용자가 시작한 원격으로 SQL Server 스크립트에서 안전 하 게 전달 될 Windows 자격 증명을 사용 하도록 설정 하려면 자격 증명을 에뮬레이트할 해야 합니다. 이 프로세스 라고 _암시 된 인증이_합니다. 이 작업을 하려면 SQL Server 컴퓨터에 R, Python 스크립트를 실행 하는 작업자 계정이 올바른 사용 권한이 있어야 합니다.

1. 열기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] R 코드를 실행 하려면 인스턴스의 관리자 권한으로 합니다.

2. 다음 스크립트를 실행합니다. 기본적으로 변경한 경우 사용자 그룹 이름 및 컴퓨터 및 인스턴스 이름을 편집 해야 합니다.

    ```SQL
    USE [master]
    GO
    
    CREATE LOGIN [computername\\SQLRUserGroup] FROM WINDOWS WITH
    DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ```

## <a name="avoid-clearing-the-workspace-while-youre-running-r-in-a-sql-compute-context"></a>SQL 계산 컨텍스트에서 R을 실행 하는 동안 작업 영역을 선택 취소 하지 마십시오.

가질 수 있습니다는 R 콘솔에서 작업할 때 작업 영역을 선택 취소 하는 것은 일반적인, 계산 컨텍스트는 SQL에서 의도 하지 않은 결과입니다.

`revoScriptConnection` SQL Server에서 호출 되는 R 세션에 대 한 정보를 포함 하는 R 작업 영역에서 개체가입니다. 그러나 R 코드의 작업 영역을 선택 취소 하는 명령을 포함 하는 경우 (예: `rm(list=ls())`), 세션 및 기타 개체는 R 작업 영역에 대 한 모든 정보의 선택도 취소 됩니다.

이 문제를 해결 SQL Server에서 R을 실행 하는 동안 변수 및 기타 개체를 무분별 하 게 삭제를 하지 마십시오. 사용 하 여 특정 변수를 삭제할 수는 **제거** 함수:

```R
remove('name1', 'name2', ...)
```

여러 변수를 삭제 하는, 경우에 임시 변수의 이름이 목록에 저장 한 다음 목록에 주기적 가비지 컬렉션을 수행 하는 것이 좋습니다.



## <a name="next-steps"></a>다음 단계

[컴퓨터 학습 서비스 문제 해결 및 알려진된 문제](machine-learning-troubleshooting-faq.md)

[기계 학습 문제 해결에 대 한 데이터 수집](data-collection-ml-troubleshooting-process.md)

[업그레이드 및 설치 FAQ](r/upgrade-and-installation-faq-sql-server-r-services.md)

[데이터베이스 엔진 연결 문제 해결](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)
