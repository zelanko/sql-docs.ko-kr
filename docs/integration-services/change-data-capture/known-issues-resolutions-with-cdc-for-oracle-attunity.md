---
title: Attunity의 Oracle용 Change Data Capture의 알려진 오류 및 해결 방법 | Microsoft Docs
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee1e8f3ae65b4a906d42a4b00644456d89f9b900
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713428"
---
# <a name="known-errors-and-resolutions-with-change-data-capture-for-oracle-by-attunity"></a>Attunity의 Oracle용 Change Data Capture의 알려진 오류 및 해결 방법
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdbmi-xxxx-xxx-md.md)]

이 토픽에서는 Oracle CDC Designer 구성 도구에서 CDC(변경 데이터 캡처) 인스턴스를 볼 때 발생하는 주요 문제 및 알려진 해결 방법을 소개합니다. 이 도구는 SQL Server 2012부터 포함된 Attunity의 Oracle용 Change Data Capture의 일부입니다. 

## <a name="bug-fixes"></a>버그 수정
너무 많은 시간 문제를 해결하기 전에 다음과 같은 알려진 문제를 방지하기 위해 Attunity Oracle용 CDC의 최신 빌드를 사용하는 것이 중요합니다.

### <a name="sql-server-2017"></a>SQL Server 2017

**버전 5.0.0.111**에는 다음의 수정 사항이 포함되어 있습니다.
- 버그 수정 - Oracle 테이블을 추가할 때 Oracle CDC Designer에서 "Incorrect syntax near the keyword 'KEY'(키워드 ‘키’ 근처의 잘못된 구문)" 오류가 발생합니다. 
- 개선 사항 - RAC에 대한 개선된 지원에는 RAC 노드가 다시 시작될 경우 처리 개선이 포함됩니다. 
- 버그 수정 - v$log의 NEXT_CHANGE# 요청으로 인해 CDC가 Oracle 10.2에서 작동하지 않습니다. 


**버전 5.0.0.93**에는 다음 수정 사항이 포함되어 있습니다. 
- Oracle 테이블을 추가할 때 Attunity Oracle용 Microsoft CDC Designer에서 "Incorrect syntax near the keyword 'KEY'(키워드 ‘키’ 근처의 잘못된 구문)" 오류가 발생합니다. 

 
### <a name="sql-server-2016"></a>SQL Server 2016

**버전 4.0.107**에는 다음 수정 사항이 포함되어 있습니다.
- 버그 수정 - Oracle 테이블을 추가할 때 Oracle CDC Designer에서 "Incorrect syntax near the keyword 'KEY'(키워드 ‘키’ 근처의 잘못된 구문)" 오류가 발생합니다.
- 개선 사항 - RAC에 대한 개선된 지원에는 RAC 노드가 다시 시작될 경우 처리 개선이 포함됩니다.
- 버그 수정 - v$log의 NEXT_CHANGE# 요청으로 인해 CDC가 Oracle 10.2에서 작동하지 않습니다.

**버전 4.0.0.95**에는 다음 수정 사항이 포함되어 있습니다. 
- 버그 수정 - Oracle 테이블을 추가할 때 Oracle CDC Designer에서 "Incorrect syntax near the keyword 'KEY'(키워드 ‘키’ 근처의 잘못된 구문)" 오류가 발생합니다.

**버전 4.0.0.88**에는 다음 수정 사항이 포함되어 있습니다.
-  Attunity CDC 인스턴스의 고급 옵션에 추가된 속성은 CDC에서 테이블이 추가되거나 제거될 때 제거됩니다. 
- __$command_id 열을 추가하는 SQL 수정 내용을 적용한 후 Attunity CDC가 작동하지 않습니다.

### <a name="sql-server-2014"></a>SQL Server 2014 

**버전 2.0.0.114**에는 다음 수정 사항이 포함되어 있습니다.
- 버그 수정 - Oracle 테이블을 추가할 때 Oracle CDC Designer에서 "Incorrect syntax near the keyword 'KEY'(키워드 ‘키’ 근처의 잘못된 구문)" 오류가 발생합니다.
- 개선 사항 - RAC에 대한 개선된 지원에는 RAC 노드가 다시 시작될 경우 처리 개선이 포함됩니다.
- 버그 수정 - v$log의 NEXT_CHANGE# 요청으로 인해 CDC가 Oracle 10.2에서 작동하지 않습니다.

**버전 2.0.0.92**에는 다음 수정 사항이 포함되어 있습니다. 
- Attunity CDC 인스턴스의 고급 옵션에 추가된 속성은 CDC에서 테이블이 추가되거나 제거될 때 제거됩니다. __$command_id 열을 추가하는 SQL 수정 내용을 적용한 후 Attunity CDC가 작동하지 않습니다.
- Oracle 테이블 cdc.table_name에 대한 메타데이터 유효성 검사가 실패했습니다. 열 column_name 인덱스가 범위를 벗어났습니다.  이 문제는 다음과 같습니다. Attunity Oracle용 CDC를 사용할 때 Oracle CDC 서비스가 중단된 상태를 표시합니다.
    - KB [2894025](https://support.microsoft.com/kb/2894025)에 설명된 대로 _SQL Server 2014 RTM용 누적 업데이트 1_에서 수정되었습니다.
- 일부 변경 사항이 누락되고 SQL Server 데이터베이스로 복제되지 않습니다. 이 문제는 테이블에 CLOB(Character Large Binary Object)가 두 개 이상 포함되고 CLOB 중 하나가 큰 값을 갖는 경우 발생합니다. 
    - KB [3029096](https://support.microsoft.com/kb/3029096)에 설명된 대로 _SQL Server 2014 SP1용 누적 업데이트 1_ 및 _SQL Server 2014 RTM용 누적 업데이트 8_에서 수정되었습니다. 
- Oracle 테이블에 Long 데이터 형식의 열이 있는 경우 Attunity의 Oracle용 Change Data Capture가 작동을 중지합니다.
    - KB [3145983](https://support.microsoft.com/kb/3145983)에 설명된 대로 _SQL Server 2014 SP1용 누적 업데이트 5_ 및 _SQL Server 2014 RTM용 누적 업데이트 12_에서 수정되었습니다.

### <a name="sql-server-2012"></a>SQL Server 2012

**버전 1.1.0.102**에는 다음 수정 사항이 포함되어 있습니다. 
 
- Attunity CDC 인스턴스의 고급 옵션에 추가된 속성은 CDC에서 테이블이 추가되거나 제거될 때 제거됩니다. __$command_id 열을 추가하는 SQL 수정 내용을 적용한 후 Attunity CDC가 작동하지 않습니다.
- Oracle 인스턴스용 CDC가 시작 시 중단되고 변경 내용을 캡처하지 않습니다. Oracle 서버 메모리는 메모리가 부족하거나 작동이 중단될 때까지 늘어날 수 있습니다.
- [2672759](https://support.microsoft.com/kb/2672759): Attunity의 Oracle용 Microsoft Change Data Capture 사용 시 오류 메시지: "ORA-00600: 내부 오류 코드". SOURCE 수준 추적을 추가하고 동일한 ORA-00600 오류가 발생하는지 확인합니다. Oracle 패치 다운로드로 수정되었습니다.
- 여러 파티션
    - Oracle 테이블에서 10개 이상의 파티션을 사용할 경우 CDC 인스턴스가 테이블의 모든 변경 내용을 캡처할 수 없습니다. Oracle 테이블이 10개가 넘는 파티션을 사용하여 정의된 경우 변경 내용은 마지막 10개 파티션에서만 캡처됩니다. _SQL Server 2012용 Service Pack 1 릴리스_에서 수정되었습니다. [SP1 기능 팩 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=35580)를 참조하세요. 
- 변경 내용이 손실됨
    - 이벤트 캡처가 무한 루프로 이동하여 새 데이터 변경 캡처를 중지할 수 있습니다(Oracle 버그 5623813 관련). Oracle RAC 환경에서 CDC 인스턴스의 중지 또는 재개를 수행하는 경우 변경 내용이 건너 뛰어지거나 손실될 수 있습니다. 즉, SQL Server 변경 데이터 캡처에서 중요한 행을 누락하게 되고 그 결과 데이터 웨어하우스 또는 구독 시스템에서 데이터 손실이 발생합니다. _SQL Server 2012용 Service Pack 1 릴리스_에서 수정되었습니다. [SP1 기능 팩 다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=35580)를 참조하세요.
- SQL 열의 두 배 너비
    - Oracle용 CDC 인스턴스를 만들 때 SQL Server에 대해 실행할 스크립트에서 가변 너비 데이터 형식 열의 길이가 스크립트에 생성된 SQL Server 테이블에서 두 배가 됩니다. 예를 들어 Oracle 테이블의 VARCHAR2(10) 열에 대한 변경 내용을 추적하려는 경우 배포 스크립트에서 SQL Server 테이블의 해당 열은 NVARCHAR(20)입니다. KB [2769673](https://support.microsoft.com/kb/2769673)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 2_ 또는 _SQL Server 2012용 누적 업데이트 5_ 중 하나에서 수정합니다. 
- DDL 데이터가 잘림
    - 라틴 문자가 아닌 문자를 포함하는 Oracle 데이터베이스에 대해 4,000바이트보다 큰 DDL(데이터 정의 언어) 문을 실행하는 경우 CDC for Oracle by Attunity에 오류가 발생합니다. 또한 오류 메시지 `ORA-01406: fetched column value was truncated.`가 표시됩니다. KB [2839806](https://support.microsoft.com/kb/2839806)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 4_에서 수정되었습니다. 
- 마지막 두 열에서 변경 내용이 손실됨
    - KB [2874879](https://support.microsoft.com/kb/2874879)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 6_에서 수정되었습니다. 
- Oracle용 CDC를 사용할 때 SQL 트랜잭션 로그 증가
     - Oracle용 Change Data Capture 인스턴스가 구성된 경우 변경된 데이터를 받는 SQL 데이터베이스에 복제로 표시된 트랜잭션이 포함된 미러링된 테이블이 있습니다. 이 동작은 Oracle용 CDC가 SQL Server용 CDC에서 사용되는 것과 유사한 기본 시스템 저장 프로시저를 사용하기 때문에 발생합니다. 그러나 Oracle용 CDC를 단독으로 사용하는 경우에는 SQL CDC 복제가 수반되지 않으므로 복제를 위해 표시된 트랜잭션을 지울 로그 판독기가 없습니다. SQL Server에서 트랜잭션을 복제할 필요가 없기 때문에 이 문서의 뒷부분에서 설명하게 될 해결 방법을 사용하여 수동으로 트랜잭션을 배포된 것으로 표시하는 것이 안전합니다. 자세한 내용은 KB [2871474](https://support.microsoft.com/kb/2871474)를 참조하세요. 
- 오류 `ORACDC000T: Error encountered at position to change event - SCN not found - EOF simulated`. KB [2883524](https://support.microsoft.com/kb/2883524)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 7_에서 수정되었습니다. 
- Oracle 테이블 cdc.table_name에 대한 메타데이터 유효성 검사가 실패했습니다. 열 column_name 인덱스가 범위를 벗어났습니다. KB [2883524](https://support.microsoft.com/kb/2883524)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 7_에서 수정되었습니다.
- SQL Server 2012에서 Attunity의 Oracle용 CDC를 사용할 때 Oracle CDC 서비스는 중단된 상태를 표시합니다. KB [2923839](https://support.microsoft.com/kb/2923839)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 8_에서 수정되었습니다.  
- 일부 변경 사항이 누락되고 SQL Server 데이터베이스로 복제되지 않습니다. 이 문제는 테이블에 CLOB(Character Large Binary Object)가 두 개 이상 포함되고 CLOB 중 하나가 큰 값을 갖는 경우 발생합니다. KB [2923839](https://support.microsoft.com/kb/2923839)에 설명된 대로 _SQL Server 2012 SP1용 누적 업데이트 8_에서 수정되었습니다.   
- Oracle 테이블에 Long 데이터 형식의 열이 있는 경우 Attunity의 Oracle용 Change Data Capture가 작동을 중지합니다. KB [3145983](https://support.microsoft.com/kb/3145983)에 설명된 대로 _SQL Server 2012 SP3용 누적 업데이트 2_ 및 _SQL 2012 SP2용 누적 업데이트 11_에서 수정되었습니다. 

## <a name="collect-detailed-logs"></a>자세한 로그 수집 

이 섹션에서는 CDC 인스턴스에서 오류 및 이벤트를 수집하는 방법을 설명합니다. 

### <a name="management-console"></a>관리 콘솔

왼쪽 창에서 CDC 인스턴스를 강조 표시된 경우 Oracle Change Data Capture Designer 관리 콘솔 내의 **상태** 메시지 필드에서 오류를 볼 수 있습니다. 

### <a name="query-trace-table"></a>쿼리 추적 테이블

SQL Server 내의 CDC 데이터베이스에서 추적 테이블을 쿼리하여 로깅된 오류를 볼 수 있습니다. 

### <a name="save-output-from-basic-logging"></a>기본 로깅의 출력 저장 

진단을 캡처하려면 Oracle Change Data Capture 관리 콘솔의 상태 탭에서 **진단 수집**을 선택합니다. 

![진단 링크 수집](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

시작 시간을 선택하고 로그 파일의 위치를 선택합니다. 그런 다음 **만들기**를 선택하여 진단 수집을 시작합니다. 

![진단 링크 수집](media/known-issues-resolutions-with-cdc-for-oracle-attunity/start-diagnostics.png)

### <a name="detailed-errors"></a>오류 세부 정보

인스턴스에 의해 수집된 추적 수준을 높이고 시나리오를 반복하여 더 자세한 로깅을 수집할 수 있습니다. 이렇게 하려면 **작업** 아래의 **속성**을 선택한 다음 **고급** 탭의 **고급 설정** 그리드에서 새 속성을 추가합니다. 속성 이름을 `trace`로 설정한 다음 값을 `SOURCE`로 설정합니다. 

![진단 링크 수집](media/known-issues-resolutions-with-cdc-for-oracle-attunity/properties.png)

오류를 재현한 다음 **진단 수집** 옵션을 선택하여 로그를 수집합니다. 

![진단 링크 수집](media/known-issues-resolutions-with-cdc-for-oracle-attunity/collect-diagnostics.png)

## <a name="ora-00942-table-of-view-does-not-exist"></a>ORA-00942 테이블 보기가 존재하지 않음 

이 오류는 CDC 인스턴스의 **상태** 메시지 필드에 표시되는 일반적인 오류입니다. 인스턴스는 여러 번 다시 시도하므로 상태 아이콘이 잠시 녹색으로 바뀌지만 그 후에는 빨간색 느낌표와 UNEXPECTED 상태와 함께 오류가 발생합니다. 

![Oracle 오류](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-error.png)

```
"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC508E:Oracle method OCIStmtExecute failed with error: ORA-00942: table or view does not exist ","source","",""

"ERROR","computername","RUNNING","IDLE",
"ORACDC518E:Failed to verify archive log mode.","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC517E:Oracle Call Interface (OCI) method failed: ORA-00942: table or view does not exist .","source","",""

"ERROR","computername","ERROR","UNEXPECTED",
"ORACDC414E:The Engine component failed with return code 1.","engine","",""
```

이 오류는 CDC 인스턴스에서 Oracle 서버로 연결하는 Oracle 계정에 시스템 로그 보기를 볼 권한이 없는 경우에 발생합니다. 

### <a name="resolution"></a>해결 방법

이 오류를 해결하려면 Oracle 데이터베이스 시스템 내에서 현재 구성된 사용자에게 적절한 권한을 부여하거나 CDC 인스턴스에서 Oracle 서버에 연결하는 데 사용되는 계정을 변경합니다. 

모든 필요한 권한 목록은 설치 프로그램 파일 폴더`C:\Program Files\Change Data Capture for Oracle by Attunity\Attunity.SqlServer.XdbCdcDesigner.chm`에 포함된 도움말 파일에 자세히 설명되어 있습니다.  전체 목록은 .chm 파일 내의 "Oracle 원본 데이터베이스에 연결"이라는 제목의 페이지를 참조하세요.

왼쪽 창에서 CDCInstance를 선택하고 **CDC Designer** 창 내의 가장 오른쪽 작업 창에서 속성 단추를 선택하여 사용자 계정을 설정할 수 있습니다. 속성 대화 상자 페이지에서 Oracle 로그 마이닝 인증 계정을 변경할 수 있습니다.

![Oracle 오류](media/known-issues-resolutions-with-cdc-for-oracle-attunity/oracle-connection.png)


  
## <a name="see-also"></a>관련 항목:  
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [변경 데이터 캡처 정보&#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [변경 데이터 작업&#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [변경 데이터 캡처 관리 및 모니터링&#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
