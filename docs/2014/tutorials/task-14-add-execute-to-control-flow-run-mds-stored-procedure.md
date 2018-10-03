---
title: '태스크 14: 추가 SQL 실행 태스크를 MDS에 대 한 저장된 프로시저를 실행 하려면 제어 흐름 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9e2f62236d844a6ded850f33207bad9da082ce62
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177293"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>태스크 14: 제어 흐름에 SQL 실행 태스크를 추가하여 MDS에 대한 저장 프로시저 실행
  데이터를 MDS의 준비 테이블에 로드한 다음에는 준비 테이블의 데이터를 MDS 데이터베이스의 적합한 테이블로 로드하기 위해 해당 테이블과 연관된 저장 프로시저를 실행합니다. 이 저장 프로시저에는 전달해야 하는 두 개의 필수 매개 변수(LogFlag 및 VersionName)가 있습니다. LogFlag는 준비 프로세스 중 트랜잭션을 기록할지 여부를 지정하고, VersionName은 모델의 버전을 나타냅니다. 참조 [준비 된 저장 프로시저](http://msdn.microsoft.com/library/hh231028.aspx) 자세한 세부 정보에 대 한 항목입니다.  
  
 이 작업에서는 준비된 데이터를 적절한 MDS 테이블로 로드하기 위해 저장 프로시저를 호출하는 SQL 실행 태스크를 제어 흐름에 추가합니다.  
  
1.  이제 전환할 합니다 **제어 흐름** 탭 합니다.  
  
2.  끌어서 놓기 **SQL 실행 태스크** 에서 합니다 **SSIS 도구 상자** 하는 **제어 흐름** 탭 합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **SQL 실행 태스크** 에 **제어 흐름** 탭을 클릭 **이름 바꾸기**합니다. 형식 **Trigger Stored Procedure to Load Data into MDS** 누릅니다 **ENTER**합니다.  
  
4.  연결 **Receive, Cleanse, 일치 및 Curate Supplier Data** 하 **Trigger Stored Procedure to Load Data** 녹색 커넥터를 사용 하 여 합니다.  
  
     ![SQL 실행 태스크에 연결](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "SQL 실행 태스크에 연결")  
  
5.  사용 하는 **변수** 창에서 다음 설정을 사용 하 여 두 개의 새로운 변수를 추가 합니다. 표시 되지 않으면 합니다 **변수** 창에서 클릭 **SSIS** 메뉴를 클릭 **변수**합니다.  
  
    |이름|데이터 형식|값|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![SSIS 변수 창](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 변수 창")  
  
6.  두 번 클릭 **저장된 프로시저를 MDS에 데이터 로드를 트리거할**합니다.  
  
7.  에 **SQL 실행 태스크 편집기** 대화 상자에서 **(local). MDS** (또는 **localhost입니다. MDS**)에 대 한 **연결**합니다.  
  
8.  형식 **EXEC [stg]. [ udp_Supplier_Leaf]???** 에 대 한 **SQL 문을**합니다. SQL Server Management Studio를 사용해서 이름을 확인할 수 있습니다.  
  
     ![실행 SQL 편집기 대화 상자-일반 설정](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "실행 SQL 편집기 대화 상자-일반 설정")  
  
9. 클릭 **매개 변수 매핑** 왼쪽 메뉴에서.  
  
10. 에 **매개 변수 매핑을** 페이지에서 클릭 **추가** 매핑을 추가 하려면. 드롭 다운 목록의 값이 올바르게 표시되도록 창을 최대화하고 열 크기를 조정합니다.  
  
11. 선택 **user:: versionname** 드롭 다운 목록에서 합니다 **변수 이름**합니다.  
  
12. 선택 **NVARCHAR** 에 대 한 **데이터 형식**합니다.  
  
13. 형식 **0** (영)에 대 한 **매개 변수 이름**합니다.  
  
14. 이전 4개 단계를 반복해서 변수를 두 개 더 추가합니다.  
  
    |변수 이름|데이터 형식(중요)|매개 변수 이름|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![SQL 실행 태스크 편집기-매개 변수 매핑](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "SQL 실행 태스크 편집기-매개 변수 매핑")  
  
15. 클릭 **확인** 닫으려면 합니다 **SQL 편집기 실행** 대화 상자.  
  
## <a name="next-step"></a>다음 단계  
 [태스크 15: SSIS 프로젝트 작성 및 실행](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
