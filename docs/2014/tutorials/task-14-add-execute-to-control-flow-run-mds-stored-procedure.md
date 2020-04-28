---
title: '태스크 14: 제어 흐름에 SQL 실행 태스크를 추가 하 여 MDS에 대 한 저장 프로시저 실행 Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8c926f2ea3d9ef9973f75764e254c5e0884836e3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177293"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>태스크 14: Control Flow에 SQL 실행 태스크를 추가하여 MDS에 대한 저장 프로시저 실행
  데이터를 MDS의 준비 테이블에 로드한 다음에는 준비 테이블의 데이터를 MDS 데이터베이스의 적합한 테이블로 로드하기 위해 해당 테이블과 연관된 저장 프로시저를 실행합니다. 이 저장 프로시저에는 전달해야 하는 두 개의 필수 매개 변수(LogFlag 및 VersionName)가 있습니다. LogFlag는 준비 프로세스 중 트랜잭션을 기록할지 여부를 지정하고, VersionName은 모델의 버전을 나타냅니다. 자세한 내용은 [준비 된 저장 프로시저](https://msdn.microsoft.com/library/hh231028.aspx) 항목을 참조 하세요.

 이 작업에서는 준비된 데이터를 적절한 MDS 테이블로 로드하기 위해 저장 프로시저를 호출하는 SQL 실행 태스크를 제어 흐름에 추가합니다.

1.  이제 **제어 흐름** 탭으로 전환 합니다.

2.  **SQL 실행 태스크** 를 **SSIS 도구 상자** 에서 **제어 흐름** 탭으로 끌어서 놓습니다.

3.  **제어 흐름** 탭에서 **SQL 실행 태스크** 를 마우스 오른쪽 단추로 클릭 하 고 **이름 바꾸기**를 클릭 합니다. **트리거 저장 프로시저를 입력 하 여 데이터를 MDS에 로드 하** 고 **enter**키를 누릅니다.

4.  **수신, 정리, 일치 및 데이터 공급자 데이터** 를 연결 하 여 녹색 커넥터를 사용 하 여 **데이터를 로드 하는 트리거 저장 프로시저** 를 연결 합니다.

     ![SQL 실행 태스크에 연결](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "SQL 실행 태스크에 연결")

5.  **변수** 창을 사용 하 여 다음 설정을 사용 하 여 두 개의 새 변수를 추가 합니다. **변수** 창이 표시 되지 않으면 메뉴 모음에서 **SSIS** 를 클릭 하 고 **변수**를 클릭 합니다.

    |Name|데이터 형식|값|
    |----------|---------------|-----------|
    |LogFlag|Int32|1|
    |VersionName|문자열|VERSION_1|

     ![SSIS 변수 창](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 변수 창")

6.  **트리거 저장 프로시저를 두 번 클릭 하 여 데이터를 MDS로 로드**합니다.

7.  **SQL 실행 태스크 편집기** 대화 상자에서 **(로컬)을 선택 합니다. MDS** (또는 **localhost) MDS**)를 **연결**합니다.

8.  **EXEC [stg]. [를 입력 합니다. udp_Supplier_Leaf]?,?,?** **SQL 문** SQL Server Management Studio를 사용해서 이름을 확인할 수 있습니다.

     ![SQL 편집기 실행 대화 상자 - 일반 설정](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "SQL 편집기 실행 대화 상자 - 일반 설정")

9. 왼쪽의 메뉴에서 **매개 변수 매핑** 을 클릭 합니다.

10. **매개 변수 매핑** 페이지에서 **추가** 를 클릭 하 여 매핑을 추가 합니다. 드롭 다운 목록의 값이 올바르게 표시되도록 창을 최대화하고 열 크기를 조정합니다.

11. **변수 이름**에 대 한 드롭다운 목록에서 **User:: versionname** 을 선택 합니다.

12. **데이터 형식**에 대해 **NVARCHAR** 를 선택 합니다.

13. **매개 변수 이름**으로 **0** 을 입력 합니다.

14. 이전 4개 단계를 반복해서 변수를 두 개 더 추가합니다.

    |변수 이름|데이터 형식(중요)|매개 변수 이름|
    |-------------------|-----------------------------|--------------------|
    |User::LogFlag|LONG|1|
    |User::BatchTag|NVARCHAR|2|

     ![SQL 실행 태스크 편집기 - 매개 변수 매핑](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "SQL 실행 태스크 편집기 - 매개 변수 매핑")

15. **확인** 을 클릭 하 여 **SQL 편집기 실행** 대화 상자를 닫습니다.

## <a name="next-step"></a>다음 단계
 [태스크 15: SSIS 프로젝트 빌드 및 실행](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)


